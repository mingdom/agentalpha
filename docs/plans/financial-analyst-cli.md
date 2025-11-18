## Goal

Build a minimal CLI MVP that allows a financial analyst to focus on one ticker (e.g., NVDA), hit a single command, and walk away with:

1. Downloaded quarterly earnings/data + key ratios via FinanceToolkit.
2. Local caching in AI-agent friendly formats (JSON/CSV) so repeated analysis is instant.
3. Console-friendly reporting that highlights the most important metrics and provides hooks for modeling or exports.

The CLI should feel interactive even though the MVP only needs to cover a single ticker per invocation. Typer is the command framework of choice, with optional use of `rich` for formatted tables/output and `typer` prompts for any missing configs.

## Scope

- Setup CLI wiring with Typer CLI app entrypoint.
- Integrate `FinanceToolkit` to fetch quarterly statements/ratios for one ticker.
- Persist fetched data locally via standard formats (JSON + CSV) and leverage the toolkit’s cache for fast reruns.
- Provide a single command `agentalpha data nvda` (or similar) that:
  * Accepts ticker, start date (default 8 quarters), and cache controls.
  * Fetches statements, historical price, and ratio data.
  * Stores raw cache to disk and exports sanitized JSON/CSV copies.
  * Prints key metrics + a summary table to the terminal.
  * Optionally opens local files for further processing.

## Architecture Overview

### CLI Layer (Typer)

- Entrypoint: `agentalpha` script loaded by Typer; single command group `data`.
- Command signature: `agentalpha data fetch --ticker NVDA --start-date 2022-01-01 --refresh`.
- Arguments:
  * `ticker` (required, default NVDA for MVP).
  * `start_date` optional (defaults to 8 quarters back).
  * `--refresh / --no-refresh` flag controlling cache refresh.
  * `--output-dir` to override default storage location (`data/nvda`).
- CLI responsibilities:
  * Validate ticker format (uppercase, alphanum).
  * Use Typer prompts if arguments missing (for future multi-ticker CLI).
  * Output progress via `rich` (progress bars / tables).

### FinanceToolkit Integration

- Instantiate as:
  ```
  toolkit = Toolkit(
      tickers=[ticker],
      api_key=FMP_API_KEY,
      quarterly=True,
      start_date=start_date,
      enforce_source="FinancialModelingPrep",
      use_cached_data=cache_path,
  )
  ```
- Primary data fetches:
  * `toolkit.get_income_statement()`, `get_balance_sheet_statement()`, `get_cash_flow_statement()` for statement history.
  * `toolkit.get_historical_data()` for price/benchmark data (needed for EV/market-based ratios).
  * `toolkit.ratios.collect_profitability_ratios()`, `collect_growth_ratios()`, `collect_valuation_ratios()` for derived metrics.
  * `toolkit.ratios.get_return_on_equity()` etc. can be used for ad-hoc values if necessary.
- Accounting for quarterly alignment and currency normalization automatically handled by the toolkit.
- Provide error handling for rate limits (retry/backoff) and fallback to cached data when necessary.
- After fetching, store DataFrames locally as JSON (via `to_json(orient='split')`) and CSV for agent-friendly format.

### Local Storage Format

- Directory layout:
  ```
  data/
    nvda/
      toolkit-cache.pkl          # FinanceToolkit pickle cache
      income_statement.json
      income_statement.csv
      balance_sheet.json
      cash_flow.json
      ratios/
        profitability.json
        valuation.json
        growth.json
        metrics.json           # aggregated metric list
      historical_price.json
      metadata.json             # {ticker, fetched_at, source}
  ```
- JSON format example: orientation `split` (index columns data) for easy DataFrame reconstruction.
- CSV exports for quick manual review / pipeline ingestion.
- Metadata file includes ticker, args, `cache_version`, `last_updated`, `source` (FMP).
- Provide optional `ai_ready` flag meaning normalized structure (list of dicts) friendly to agents.
- Use consistent naming (e.g., `yyyy-mm-dd.json`) for future multi-quarter snapshots.

### Caching Strategy

- FinanceToolkit already pickles combined dataset when `use_cached_data=True`; we will reuse this but also mirror outputs in JSON/CSV for AI usage.
- CLI ensures new data only fetched when:
  * `--refresh` flag set.
  * Cache missing or expired (e.g., older than 90 days or last quarter change).
- Cache path defaults to `data/<ticker>/toolkit-cache.pkl`.
- On CLI start, report cache status (found, age) and whether refresh needed.
- Optionally perform `hashlib.sha256` on outputs for integrity checks (future).

### Output Reporting

- Use `rich.table.Table` for CLI summary showing:
  * Latest revenue, EPS, EBIT, EBITDA, FCF.
  * Key ratios: PE, EV/EBITDA, ROIC, Gross Margin, Debt/Equity, Revenue CAGR.
  * Last 8 quarters of EPS + revenue growth (sparklines optional via `rich`).
- Provide textual explanation of data source, next refresh point, and stored file paths.
- After CLI run, print:
  * "Data persisted to ... (JSON/CSV + cache path)."
  * "Use `agentalpha data --help` for next steps."
- Optionally show `rich.traceback` and friendly errors for API issues.

## Modeling & Next Steps (Post-MVP)

- While MVP focuses on data ingestion/display, we design the CLI to eventually integrate:
  * DCF modeling modules (import statement & ratio outputs).
  * Monte Carlo path planning using `numpy`/`pandas`.
  * Export `scenarios.json` summarizing assumptions/outcomes.
- Consider `typer` subcommands `model` / `scenario` after data flows stabilized.
- Build `analysis/` folder to hold modeling logic that consumes the cached JSON/CSV.

## Key Decisions

1. **FinanceToolkit for data:** Transparent calculations, normalized statements, built-in ratio collectors, caching; we enforce the FMP data source for consistency.
2. **Typer CLI:** Fast developer ergonomics and future extensibility.
3. **Storage format:** JSON (orient split) + CSV for DataFrame compatibility, plus metadata for agents; cache file respects toolkit's existing pickle.
4. **Single ticker focus:** MVP simplifies interface and reduces API pressure while still proving out caching + modeling path.
5. **Local cache awareness:** CLI reports age & refresh need; `--refresh` ensures analysts can force new data if quarter rolled.

## Open Questions / Future Considerations

- Should we version the cache per quarter to allow historical reruns?
- Do we need a schema validator (e.g., `pydantic`) for local JSON outputs to ensure AI agents can rely on expected fields?
- How granular should refresh policies be? Quarterly baseline vs. explicit `--refresh`.
- Do we want to stream data to remote storage (S3/DB) later, or keep strictly local for now?
- In what format should we expose modeling outputs for agents? (Maybe `scenario_summary.json`.)

## Summary

The MVP CLI will deliver instant access to NVDA's recent statements and ratios via FinanceToolkit, persist the data as JSON/CSV for reuse and agent consumption, and provide a polished Typer/Rich interface that confirms storage and readiness for modeling. Once validated, the same pipeline enables us to add multi-ticker support, run DCF/Monte Carlo scenarios, and orchestrate more involved reporting flows. continuous automation or cron jobs rerunning `agentalpha data fetch` after each earning release can keep caches current for the team. Let's start with the script, verify the outputs, and then expand modeling commands in the next iteration.
