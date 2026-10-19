# When will the bus arrive?

A six-week undergraduate project using Gainesville RTS records to explore data cleaning, feature engineering, and machine learning.

**Main question:** Can we predict the time between consecutive bus stops better than using the usual travel time for that stop pair?

## Start here

1. Follow [the software setup guide](docs/Student_Setup_Guide.pdf).
2. Read [the student project guide](docs/Project_Guide.pdf).
3. Open the Route 7 workbook in `data/raw/` and inspect its columns, dates, and missing values.
4. Review the [data notes and source credits](data/README.md) before cleaning or modeling.

All four available route workbooks are included. Start with **Route 7**, then apply your pipeline to **Routes 3 and 11**. **Route 711** is an optional comparison with different date coverage.

## What data is included?

| Route | Raw records | Distinct observed dates | Date range |
| --- | ---: | ---: | --- |
| 7 | 14,685 | 17 | March 1–23, 2023 |
| 3 | 8,642 | 17 | March 1–23, 2023 |
| 11 | 23,365 | 17 | March 1–23, 2023 |
| 711 | 4,076 | 7 | March 4–19, 2023 |

These are **50,768 raw stop records**, not 50,768 verified journeys or model examples. The date ranges contain gaps and do not represent complete months. These are historical city RTS records, not UF Campus Connector data.

## What are we predicting?

For verified consecutive stops A and B on the same journey:

```text
Travel time = arrival at B − arrival at A
Predicted arrival at B = arrival at A + predicted travel time
```

Each training example will represent a stop pair. Predict travel time in seconds, then convert it to an arrival time. The files have no explicit trip ID, so checking journey boundaries is an important part of the project.

## Six-week plan

| Week | Focus |
| --- | --- |
| 1 | Install tools and explore Route 7. |
| 2 | Clean records, identify journeys, and verify stop pairs. |
| 3 | Split by date and build a historical-median baseline. |
| 4 | Fit a simple model and try an extra feature. |
| 5 | Investigate errors; expand to Routes 3 and 11 if ready. |
| 6 | Evaluate on held-out dates and present findings. |

Use earlier dates for training and later dates for validation/testing. Do not randomly scatter stops from the same journey across splits. A baseline that wins is still a useful result if you explain it.

## Repository layout

```text
docs/              Student PDFs and editable LaTeX sources
data/raw/          Original route workbooks; keep unchanged
data/README.md     Column definitions, limitations, and data credits
notebooks/         Student exploration, cleaning, and modeling notebooks
src/               Reusable Python functions
requirements.txt   Packages used in this project
```

The notebooks and source folders are starting places; no cleaned dataset, trained model, or performance result is provided yet. An API key is not required for these downloaded files.

## Python packages

The setup guide provides copy-and-paste installation commands. Alternatively, after creating `.venv`, install this repository's package list from its root:

Windows PowerShell:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

macOS terminal:

```bash
./.venv/bin/python -m pip install -r requirements.txt
```

Select the project's `.venv` as the Jupyter notebook kernel. The package list is not version-pinned; record installed versions for your final submission.

## Data credit

Ride-check datasets were deposited by **Richard Borzi, University of Florida**, with data supplied by **Gainesville RTS**, under **CC BY 4.0**. See [data/README.md](data/README.md) for individual source links and license details. Preserve these credits when sharing modified data. The dataset license applies to the sourced data; it does not automatically license new student code.
