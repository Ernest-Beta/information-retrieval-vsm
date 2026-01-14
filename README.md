# Information Retrieval — Vector Space Model (TF-IDF) with Elasticsearch

This project implements a classic **Information Retrieval (IR)** baseline using the **Vector Space Model (VSM)** with **TF-IDF-style scoring** on top of **Elasticsearch**.  
It indexes a document collection, runs a set of queries, retrieves the top results, and exports rankings in **TREC run format** for evaluation.

## What this project does

- Reads a document corpus from **CSV**
- Converts documents to JSON and **indexes** them into **Elasticsearch**
- Uses a VSM/TF-IDF style similarity (via Elasticsearch configuration) to score documents
- Reads queries from **CSV**
- Retrieves the **top-k** results for each query
- Writes **TREC-formatted run files** for standard IR evaluation (e.g., `trec_eval`)

## Output

The notebook generates TREC run files for multiple cutoffs (example):
- `k = 20`
- `k = 30`
- `k = 50`

Each run file contains lines in the standard format:

`<query_id> Q0 <doc_id> <rank> <score> <run_name>`

These files can be used directly with tools like **trec_eval** to compute metrics such as MAP, nDCG, Precision@k, etc.

## Project structure

- `VSM_IR_model.ipynb` — main notebook (end-to-end pipeline)
- `documents.csv` — input corpus (expected columns like `ID`, `Text`)
- `queries.csv` — input queries (expected columns like `ID`, `Text`)
- `trec_eval/` — generated run files (TREC format)

> Note: `documents.csv` and `queries.csv` may not be included if they are large or private.

## Requirements

- Python 3.x
- A running Elasticsearch instance (local)
- Python packages:
  - `elasticsearch`
  - `pandas`

## Setup

### 1) Start Elasticsearch locally
Make sure Elasticsearch is running on:

`http://localhost:9200`

You can verify it by opening that URL in your browser.

### 2) Install dependencies
```bash
pip install pandas elasticsearch
