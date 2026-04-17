# Omics Explorer

A Python tool for loading, describing, interpreting, and quality-checking any single omics data file. Built during the NOD BC2 2026 coding bootcamp (Week 2).

## What it does

Point it at any omics CSV or Excel file and get back:

- **Data dictionary** — dtype, range, missingness, skewness for every column
- **Automatic column labelling** — identifies proteins (Olink NPX), metadata (age, sex, diagnosis), and unknowns
- **Quality warnings** — 7 flag types: missingness, outliers, LOD floor artifacts, low variance, high skewness, duplicate rows
- **Distribution plots** — metadata bar/histograms + protein NPX overview + individual protein grid
- **Self-contained HTML report** — one file, opens in any browser, includes collapsible explanations for every section

## Demo

```python
# Change this one line — everything else runs automatically
FILE_PATH = "path/to/your/data.csv"

generate_report(FILE_PATH)
# → opens omics_explorer_report.html in your browser
```

## Files

| File | Description |
|------|-------------|
| `omics_explorer.ipynb` | Main notebook — function definitions + step-by-step execution |
| `omics_explorer_report.html` | Pre-generated demo report (STARNET proteomics) |
| `starnet_data_dictionary.json` | Exported data dictionary from demo run |
| `presentation.html` | NOD BC2 presentation (Reveal.js) |

## Correcting misclassified columns

If a column is labelled incorrectly, add it to the `OVERRIDES` dict at the top of the `interpret_columns` cell:

```python
OVERRIDES = {
    "uPA": "protein_npx",   # was misclassified as metadata
}
```

Valid types: `protein_npx`, `sample_metadata`, `categorical_metadata`, `unknown`

## Roadmap

| Phase | Scope |
|-------|-------|
| v1 (now) | Single CSV/Excel, Olink NPX, offline rule-based interpretation |
| v2 | Raw Olink file support, platform detection, Streamlit wrapper |
| v3 | Schema comparison across datasets, protein name harmonization |
| v4 | Batch QC + correction (ComBat, ComBatSeq) |
| v5 | SQL schema generation → AWS Athena |
| v6 | External dataset auto-ingestion pipeline (PRECAD2, KORA, GEO) |
| v8 | Claude API column interpretation |

## Context

Built as the MVP layer of a larger goal: a queryable SQL database over the [STARNET](https://www.nature.com/articles/s41588-021-00949-1) multi-omics library (26 TB, ~28 000 files, 6 omics layers, ~1 800 participants). The data dictionary exported by this tool maps directly to a SQL schema in Phase 3.

**Lab:** Björkegren Lab, Karolinska Institutet  
