# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** AI20K-2A202600421  
**Student Email:** lylyphan1104@gmail.com  
**Name:** Phan Anh Ly Ly

## Overview

This lab implements a simple ETL pipeline for product data and demonstrates why data quality matters for AI systems. The pipeline reads raw JSON data, removes invalid records, applies a small business transformation, and saves the cleaned output to CSV. After that, the project compares an agent's answer when it uses clean data versus garbage data.

## What I Completed

- Built the ETL flow in `solution.py` with `extract`, `validate`, `transform`, and `load`.
- Dropped invalid records with non-positive price or empty category.
- Standardized `category` to Title Case.
- Added `discounted_price` with a 10% discount.
- Added `processed_at` timestamp for observability.
- Ran an agent simulation on clean data and garbage data, then documented the outcome in `experiment_report.md`.

## How to Run

### Prerequisites

Install the required packages:

```bash
pip install pandas pytest
```

### Run the ETL Pipeline

```bash
python solution.py
```

Expected result:

- Input file: `raw_data.json`
- Output file: `processed_data.csv`
- Validation log shows how many records were kept and dropped

### Run the Agent Stress Test

```bash
python agent_simulation.py
```

This script compares the agent response when using:

- Clean data from `processed_data.csv`
- Garbage data from `garbage_data.csv`

## Project Structure

```text
solution.py
agent_simulation.py
raw_data.json
processed_data.csv
garbage_data.csv
experiment_report.md
README.md
tests/test_autograder.py
```

## Results Summary

- Raw records: 5
- Valid records kept: 3
- Invalid records dropped: 2
- Dropped reasons: negative price and missing category

The cleaned output keeps only trustworthy rows such as `Laptop`, `Chair`, and `Monitor`. In the stress test, the agent gives a sensible answer with clean data, but it chooses an unrealistic item from the garbage dataset because the bad data includes an extreme outlier (`Nuclear Reactor` at `999999`).

## Notes

On Windows, if `processed_data.csv` is open in another application such as Excel, the script may fail to overwrite it. Closing that file before rerunning the pipeline avoids the permission issue.
