## Context

We are evaluating how to build a repeatable financial analysis workflow for a specific portfolio holding (e.g., NVDA) that lets us:

1. Pull the last ~8 quarters of earnings and statement history.
2. Collect the core valuation, growth, and profitability metrics that investors routinely monitor.
3. Cache or persist the data locally because quarterly disclosures only roll once every few months.
4. Layer on scenario-based fair-price modeling (e.g., DCF with multiple growth paths, Monte Carlo, etc.) once the data is available.

We already have an `FMP_API_KEY` in the `.env` (ignored), so the choice is between calling the Financial Modeling Prep API directly or leveraging the FinanceToolkit wrapper described in `docs/financetoolkit-readme.md`.

## Requirements

- **Data freshness**: Weekly or hourly pulls are not necessary once the latest quarter is downloaded, but we do still want the ability to refresh after each earnings release.
- **Metrics coverage**: Earnings data, cash flow, balance sheet, and derived metrics such as PE/EV/FCF, ROIC, revenue/earnings growth, margin trends, etc.
- **Local cache**: A deterministic cache store so we do not hammer FMP limits when rerunning the same analysis.
- **Extensibility**: We will want to layer modeling and simulation code that references these datasets quickly.
- **Transparency**: Ability to audit the formulas behind each metric to verify they match our investment methodology.

## Option A: Direct FMP API

### Architecture

1. Build a lightweight client that hits FMP endpoints:
   - `/financials/income-statement` (quarterly) for earnings.
   - `/financials/balance-sheet-statement` and `/financials/cash-flow-statement` (quarterly) for statements.
   - `/ratios` or `/ratios-ttm` for per-period metrics.
   - `/historical-price-full/quote` for price and volume to calculate market-cap-based metrics.
2. Respect rate limits (250/min free) by batching requests (e.g., fetch all statements for NVDA at once and store locally before computing ratios).
3. Store the JSON response in a structured cache (e.g., `data/fmp-cache/nvda/{endpoint}.json` plus metadata such as `fetched_at`). Provide a refresh TTL (default 8 weeks for statements) and a manual force-refresh command.
4. Build small helper functions to derive metrics we care about if FMP doesn’t already expose them (e.g., trailing 12-month EBITDA margin, normalized free cash flow).

### Caching & Storage

- Auto-persist every response to disk with timestamp + API query parameters.
- Keep a lightweight manifest to know when each quarter was fetched and whether it needs refresh.
- When re-running analysis for NVDA, load cached JSON instead of hitting the API and only fetch missing quarters.

### Modeling & Simulation

- Build a modeling module that ingests the cached statements and price history.
- From the historical metrics, derive baseline assumptions (growth, margins, reinvestment) and provide knobs for scenario overrides (bull/bear cases).
- Use deterministic DCF first, then optionally run Monte Carlo with distributions on revenue growth, margin expansion, discount rate.
- Expose fair value outputs plus scenario ranges for reporting.

### Pros

- Full control over the exact data we request and formulas we use.
- Smaller dependency surface; we are only talking to one API.
- Can optimize caching and rate-limit handling specific to our workflow.

### Cons

- Need to re-implement many standard ratios and normalization steps.
- Data standardization (calendar aligning, currency conversion, trailing/growth helpers) all fall on us.
- Slightly longer time to prototype since we must stitch endpoints ourselves.

## Option B: FinanceToolkit

### Architecture

1. Install `financetoolkit` and initialize with our tickers and the existing `FMP_API_KEY`.
2. Use the toolkit's methods:
   - `get_income_statement`, `get_balance_sheet_statement`, `get_cash_flow_statement` with `quarterly=True` and `start_date` tuned to cover the last 8 quarters.
   - `ratios.collect_*` helpers (profitability, growth, valuation) to pull the full set of metrics we want.
3. The toolkit already:
   - Normalizes statements (calendar alignment, currency adjustment) before returning results (`docs/financetoolkit-readme.md:315-327`).
   - Exposes trailing/growth helpers plus a trailing parameter to compute TTM metrics (`docs/financetoolkit-readme.md:3229-3231`).
   - Supports caching via `use_cached_data=True` to pickle the data for reuse (`docs/financetoolkit-readme.md:3233-3249`).
   - Defaults to FMP but falls back to Yahoo if FMP fails unless we set `enforce_source="FinancialModelingPrep"` to guarantee consistency (`docs/financetoolkit-readme.md:54`).

### Caching & Storage

- Use `use_cached_data=True` to let the toolkit pickle the last fetched dataset to disk; we can also point it at a custom folder (our `data/toolkit-cache/` location) and versioned names for NVDA per quarter.
- On subsequent runs, initialize the toolkit with `use_cached_data=True` and bypass the network when the cache exists.
- If we need a refresh, pass a `force_refresh=True` (or delete the pickle) before reinitializing.

### Modeling & Simulation

- Extract the normalized statements from the toolkit’s DataFrames and pipe them into our scenario engine.
- Combine with `ratios.collect_*` outputs to parameterize projected growth or margin assumptions.
- Use the same modeling pipeline (DCF + Monte Carlo) but rely on the toolkit’s normalized data tables rather than building derived datasets manually.

### Pros

- Rapid prototyping; a single `Toolkit` object gives us all statements, hundreds of metrics, and optionally historical price/benchmarks.
- Built-in normalization, trailing/growth helpers, and caching reduce boilerplate.
- Transparency in metric formulas preserves auditability (`docs/financetoolkit-readme.md:3-10`).

### Cons

- Adds an external dependency whose internals we need to trust (although open-source and transparent).
- Fallback to Yahoo needs to be disabled to avoid inconsistent sources; we must pass `enforce_source="FinancialModelingPrep"`.
- Less control over exact API call sequencing if we need to profile request performance.

## Recommendation & Execution Plan

Given the goal—reproducible, metric-rich analysis of NVDA with caching and easy scenario modeling—the FinanceToolkit offers the most productive starting point. It already normalizes statements, calculates dozens of metrics, and caches data via pickles while still allowing us to lock the data source to FMP. That said, we keep the option to drop to the direct API later if we hit limitations (e.g., needing a new endpoint or controlling rate-limiting more precisely).

### Next steps

1. Add a `scripts/` or `analysis/` module that instantiates `Toolkit(["NVDA"], api_key=FMP_API_KEY, quarterly=True, start_date=<24 months ago>, enforce_source="FinancialModelingPrep", use_cached_data="data/toolkit-cache/nvda.pkl")`.
2. Fetch statements + ratios and store the resulting DataFrames under `data/structured/nvda/`.
3. Build the modeling layer that:
   - Ingests cached DataFrames for NVDA and constructs baseline assumptions (growth/margins).
   - Runs a deterministic DCF to compute fair value and overlays Monte Carlo/what-if for revenue growth and margin drivers.
   - Outputs a report summarizing scenarios plus current market price to highlight upside/downside.
4. Automate cache refresh: when new earnings drop, rerun the toolkit with `force_refresh=True` to repickle the dataset.
5. If we eventually need endpoints outside the toolkit’s coverage, write a small FMP client for those endpoints and merge the results with the toolkit cache.

This approach keeps the early iterations focused on analysis, lets us reuse the toolkit’s transparent math (or inspect it if we need to), and ensures we can pivot to direct FMP calls in future phases if a dependency gap appears.
