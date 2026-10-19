# Data notes and credits

## Included original workbooks

| File | Route | Raw rows | Dates | Source |
| --- | --- | ---: | ---: | --- |
| `raw/RTS_Route7_March2023.xlsx` | 7 | 14,685 | 17 | [Zenodo 10034933](https://zenodo.org/records/10034933) |
| `raw/RTS_Route3_Spring2023.xlsx` | 3 | 8,642 | 17 | [Zenodo 10034688](https://zenodo.org/records/10034688) |
| `raw/RTS_Route11_Spring2023.xlsx` | 11 | 23,365 | 17 | [Zenodo 10034723](https://zenodo.org/records/10034723) |
| `raw/RTS_Route711_Spring2023.xlsx` | 711 | 4,076 | 7 | [Zenodo 10034622](https://zenodo.org/records/10034622) |

**Creator/depositor:** Richard Borzi, University of Florida. The repository provenance describes data requested from and supplied by Gainesville RTS.

**License:** [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/). Credit the author and source records, link the license, and identify changes when redistributing transformed data. Workbooks in this folder are copied unchanged from the downloaded originals.

Inventory checked locally October 18, 2026. Routes 3, 7, and 11 span March 1–23, 2023, with 17 distinct observed dates each. Route 711 spans March 4–19, with seven dates. These are incomplete observational samples, not a full month or year of operations.

## Original columns

One row represents a recorded bus stop event. All four files have these 15 columns:

| Column | Description / handling |
| --- | --- |
| Route | Route label. Retain it and derive a categorical route ID. |
| Stop ID | Stop identifier; treat as a label. |
| Stop Name | Recorded stop name. |
| Stop Seq ID | Stop sequence position; useful for checking continuity. |
| Day of Week | Recorded weekday; compare against the parsed date. |
| Date | Recorded date; check calendar-date versus service-day interpretation. |
| Arrive | Arrival clock time; combine with Date and inspect midnight crossings. |
| Passenger On | Recorded boardings. |
| Passenger Off | Recorded alightings. |
| Passenger Load | Recorded load; verify timing and consistency. |
| Passenger Miles | Passenger-distance measure; verify definition and units. |
| Interstop Distance | Reported distance; verify units and which segment it describes. |
| Bus | Vehicle ID, not a journey ID. |
| Lat. | Recorded latitude; inspect validity and consistency. |
| Long. | Recorded longitude; inspect validity and consistency. |

## Important cleaning questions

- No explicit trip ID is provided. A bus may run many journeys in one day. Validate boundaries and expected stop order before pairing arrivals.
- Inspect repeated date/bus/stop/arrival keys. Excess repeats: Route 7 = 440; Route 3 = 243; Route 11 = 727; Route 711 = 114. These flags are not proof that every repeated row should be deleted.
- Missing values do not automatically mean zero. Keep an exclusion log and original row references.
- Travel time between arrivals may include boarding, waiting, and driving. It is not pure driving time.
- Passenger counts at the prediction stop may only be available after arrival. Leave them out of the initial arrival-at-A model.
- Keep routes distinct when combining files. A similar route label does not establish the same service pattern or direction.
- Learn medians, missing-value replacements, and preprocessing from training data only. Do not use future arrivals as predictors.

## Suggested first modeling table

Keep route, service date, bus ID, inferred journey ID, from-stop, to-stop, arrival A, arrival B, and travel time in seconds. Use hour of day and day of week as initial features. Keep arrival B for label creation and auditing, not as a model input.

Optional weather, GTFS, and demand datasets are not included in this starter package. Finish a reliable Route 7 pipeline before expanding.
