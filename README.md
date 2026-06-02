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

Open `analysis.ipynb` and run all cells top-to-bottom. The notebook expects the
data file at `data/Yellow_Taxi_Assignment.csv` relative to the project root,
which is the working directory Jupyter uses when launched from here.

## Files

| File | Purpose |
|------|---------|
| `notebooks/analysis.ipynb` | Final deliverable — management summary + 13 analysis sections with charts |
| `notebooks/exploration.ipynb` | Earlier EDA roughwork (schema, dirty-data audit, year distribution) |
| `data/Yellow_Taxi_Assignment.csv` | Source data — not committed, must be placed here manually |
| `pyproject.toml` | Project metadata and direct dependencies |
| `uv.lock` | Locked dependency tree for exact reproducibility |
| `.python-version` | Python version pin (3.12) read by uv |
| `requirements.txt` | Pip-compatible export for non-uv environments |

## Dataset

Standard TLC Yellow Taxi schema (19 columns). The sample is stratified by year
— approximately equal trip counts per year — so **cross-year rate metrics are
comparable but absolute volume comparisons are not**.

Columns that are empty in early years and require special handling:
- `congestion_surcharge` — introduced Feb 2019; nulls coerced to 0 for 2018
- `airport_fee` — arrives as `VARCHAR` due to early nulls; cast to `DOUBLE`
