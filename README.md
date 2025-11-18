# AgentAlpha Research Notebook

AgentAlpha is a working directory for developing and running agentic workflows that support equity research. The goals are to:

1. Curate high-quality prompts for specialist research agents.
2. Process an inbox of earnings reports, filings, and articles using those agents to extract signals.
3. Pull fundamentals, earnings, and market data to build and refresh local dossiers that agents can reason over.

## Repository layout

- `agent/`: Stable analyst personas and reporting templates.
- `inbox/`: Raw notes, prompts, and source materials awaiting triage.
- `README.md`: Project overview, workflow sketch, and next steps.

## Data sources

- **Financial Modeling Prep (FMP)**: fundamentals, earnings calendars, historical statements, and transcripts.
- **Polygon.io**: options chains, implied volatility metrics, trades/quotes for market color.

## Workflow concept

1. **Inbox intake**: Drop reports, call notes, and links into `inbox/` with timestamps.
2. **Prompted extraction**: Run analyst agents against inbox items to summarize, tag risks/opportunities, and generate follow-up questions.
3. **Data fetch**: Pull company-level fundamentals and recent earnings data from FMP; pull options data from Polygon to gauge sentiment/positioning.
4. **Dossier build**: Normalize fetched data into local storage (e.g., Parquet/SQLite) that agents can query; cache source metadata for traceability.
5. **Thesis tracking**: Record a thesis with explicit validity criteria, then automatically re-evaluate after each earnings/new data drop.
6. **Task routing**: Open todos for missing data, unanswered questions, or degraded thesis confidence.

## Implementation sketch

- **Configuration**: Store FMP and Polygon API keys in environment variables (see `.env.example` as a starting point).
- **Data layer**: Small data-access module to fetch and persist fundamental, earnings, and options datasets; prefer append-only tables with freshness timestamps.
- **Agents**: Prompt libraries for different tasks—intake triage, transcript summarization, risk scoring, and thesis validation. Keep persona prompts versioned in `agent/`.
- **Pipelines**: Scripts/notebooks to run inbox processing and data refreshes (e.g., `make ingest` or `make refresh` once implemented).
- **Outputs**: Store structured summaries and thesis updates alongside references back to source docs and API pulls.

## Suggested next steps

- Define the core data schema for fundamentals, earnings events, options snapshots, and thesis states.
- Add lightweight CLI tasks to fetch data for a given ticker and update local caches.
- Formalize the thesis evaluation template (criteria, triggers, confidence scoring) and wire it to refreshed data.
- Set up linting/tests in a `Makefile` for reproducible runs (e.g., `make lint`, `make test`).

