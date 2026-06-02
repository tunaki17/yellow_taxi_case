# NYC Yellow Taxi — Data Analyst Assignment

Exploratory analysis of a stratified 2018–2023 sample (~305,000 trips) of NYC
TLC Yellow Taxi records. Built with **Polars + DuckDB**.

## Reproducing the environment

This project uses [uv](https://docs.astral.sh/uv/) to pin Python 3.12 and lock
all dependencies.

**With uv (recommended):**

```bash
uv sync
uv run jupyter lab
```

**With plain pip (Python 3.12 required):**

```bash
python3 -m pip install -r requirements.txt
jupyter lab
```

Open `notebooks/analysis.ipynb` and run all cells top-to-bottom. The notebook expects the
data file at `data/Yellow_Taxi_Assignment.csv` relative to the project root,
which is the working directory Jupyter uses when launched from here.

## Pre-rendered reports

**No need to run code — view the analysis directly:**

The pre-rendered HTML reports in the `reports/` directory can be opened directly in any browser:

| Report | Contents |
|--------|----------|
| [`reports/analysis.html`](reports/analysis.html) | Final deliverable — management summary + 13 analysis sections with charts |
| [`reports/exploration.html`](reports/exploration.html) | EDA roughwork — schema inspection, dirty-data audit, year distribution |

Simply click the link above or download the HTML file and open in your browser. No setup required.

## Files

| File | Purpose |
|------|---------|
| `notebooks/analysis.ipynb` | Final deliverable — source notebook |
| `notebooks/exploration.ipynb` | Earlier EDA roughwork — source notebook |
| `reports/analysis.html` | Pre-rendered HTML export of the analysis notebook |
| `reports/exploration.html` | Pre-rendered HTML export of the exploration notebook |
| `data/Yellow_Taxi_Assignment.csv` | Source data — not committed (add manually from TLC data source) |
| `pyproject.toml` | Project metadata and direct dependencies |
| `uv.lock` | Locked dependency tree for exact reproducibility |
| `.python-version` | Python version pin (3.12) read by uv |
| `requirements.txt` | Pip-compatible export for non-uv environments |
| `.gitignore` | Excludes CSV data, Jupyter cache, and OS files |

## Dataset

Standard TLC Yellow Taxi schema (19 columns). The sample is stratified by year
— approximately equal trip counts per year — so **cross-year rate metrics are
comparable but absolute volume comparisons are not**.

Columns that are empty in early years and require special handling:
- `congestion_surcharge` — introduced Feb 2019; nulls coerced to 0 for 2018
- `airport_fee` — arrives as `VARCHAR` due to early nulls; cast to `DOUBLE`
