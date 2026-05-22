# The Eurovision Career-Bump Effect (2015–2025)

A data project for **Data Projects — Albert School**.
**Team:** Marta Prandin + teammate.

> **Does placing top-10 at Eurovision actually launch a music career?**

We combined two data sources — the **MusicBrainz API** (artist discographies) and **Wikipedia scraping** (artist bios) — to measure whether Eurovision top-10 finishers from 2015 to 2025 release more music *after* the contest than *before*.

## Headline finding

![Headline chart](reports/figures/chart_headline.png)

The career bump is **real but concentrated at the podium**: winners (+0.4 releases/yr) and especially runners-up (+0.9/yr) increase their output after Eurovision, while mid-table finishers (4th–10th) actually release slightly less (−0.5/yr). Activity spikes in the Eurovision year and fades within 2–3 years — **it's the platform, not the trophy, that matters.**

## Three key findings

1. **A short-term spike, not a permanent change.** Release activity jumps from ~1.5/yr to ~4.6 in the Eurovision year, stays elevated for two years, then fades.
2. **Real on average, but not universal.** The bump-ratio distribution is heavily right-skewed — many artists release *less* afterwards; a minority drive the average up.
3. **Concentrated at the podium.** Reaching the top 3 matters; the exact rank barely does (individual trend slope ≈ −0.10).

## How to reproduce

```bash
python -m venv .venv
source .venv/bin/activate          # macOS / Linux
pip install -r requirements.txt
jupyter lab    # or open the notebooks in Google Colab
```

Run the notebooks in order:

| Notebook | What it does | Output |
|---|---|---|
| `notebooks/01_api_collection.ipynb` | MusicBrainz API → artist discographies | `data/raw/eurovision_artists_discography_*.csv` + raw JSON |
| `notebooks/02_scraping.ipynb` | Wikipedia scrape → artist bios | `data/raw/eurovision_artist_bios_*.csv` (+ .parquet) |
| `notebooks/03_cleaning.ipynb` | Clean + feature-engineer | `data/processed/clean_artists_*.csv`, `clean_releases_*.csv` |
| `notebooks/04_eda_viz.ipynb` | Exploratory analysis + charts | (figures) |
| `notebooks/05_final_report.ipynb` | End-to-end narrative | (the story) |

> Notebooks 01–02 fetch live data; 03–05 read from the saved files, so you can re-run the analysis without re-hitting the API or Wikipedia.

## Repository structure

```
Data-Analytics-Project/
├── data/
│   ├── raw/          # API + scraped snapshots (timestamped)
│   └── processed/    # cleaned analytical tables
├── notebooks/        # 01 → 05, in order
├── reports/figures/  # exported charts
├── 01_project_canvas.pdf
├── README.md
├── requirements.txt
└── .gitignore
```

## Data sources & ethics

- **MusicBrainz API** — no key required; identified via a descriptive User-Agent; 1 request/sec.
- **Wikipedia** — text licensed CC-BY-SA 3.0; scraped politely (User-Agent, 1s delay); robots.txt checked.
- No personal data: all subjects are public-figure performers. No API keys or secrets are committed (`.env` is gitignored).

## Limitations

Small sample (~99 artists), MusicBrainz coverage varies by country, correlation ≠ causation, recent finishers are right-censored, and ~1/3 of artists lacked usable genre data. See `05_final_report.ipynb` for the full discussion.

## Authors

Marta Prandin + teammate — Albert School, 2026.
