# Scraping to KPI

Turns raw scraped job postings into one defensible KPI: a local LLM (Ollama) extracts
each posting's skills, a script aggregates them, and a GitHub Pages dashboard shows the
result.

Raw postings (`data/jobs_sample.csv`) and per-posting extractions (`data/extracted.json`)
stay local and are gitignored. Only the aggregate `docs/data/kpi.json` is published.

Everything runs locally, by hand: there is no GitHub Action, because the LLM step needs
a local model.
