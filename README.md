# Cyclistic Bike-Share Analysis

**Author:** Jose Nodarse  
**Tools:** Python, pandas, matplotlib, Jupyter Notebook  
**Period analyzed:** Calendar year 2019

## Project overview

This Google Data Analytics Professional Certificate capstone examines how casual riders and annual members use a bike-share service differently. Using 3.8 million recorded trips, the analysis compares trip durations, departure hours, weekdays and weekends, and monthly activity.

Cyclistic is a fictional company used in the assignment. Historical Divvy trip records provide the data for the analysis. The business objective is to identify patterns that can inform research and experiments aimed at increasing annual memberships.

## Business questions

- How do typical trip durations differ between casual and member trips?
- How do departure patterns differ by hour, day of week, and month?
- What share of recorded trips belongs to each group?
- How much do unusually long durations affect the results?

The analysis describes observed behavior. It does not establish why riders choose a membership or whether a proposed campaign will increase conversions.

## Data

Four quarterly CSV files contain **3,818,004 trips beginning in 2019**:

| Source quarter | Recorded trips |
| --- | ---: |
| Q1 | 365,069 |
| Q2 | 1,108,163 |
| Q3 | 1,640,718 |
| Q4 | 704,054 |

Relevant fields include trip ID, start and end timestamps, reported duration, station identifiers, and user type. Source labels are standardized from `Customer` to `Casual` and from `Subscriber` to `Member`.

The records represent trips, not unique customers. Demographic fields are not used in the analysis.

## Analytical workflow

1. Import quarterly records and explicitly standardize column names.
2. Combine quarters while retaining a source-quarter field.
3. Convert timestamps and reported durations into usable types.
4. Check duplicate IDs, missing values, date coverage, user types, and duration anomalies.
5. Derive departure-hour, weekday, month, and duration-in-minutes fields.
6. Compare counts, within-group percentages, daily averages, and duration distributions.
7. Compare baseline duration summaries with summaries restricted to trips lasting at most 24 hours.
8. Export summary tables and visualizations for reporting.

## Key findings

The baseline results below retain all recorded trips and use the reported duration field.

| Measure | Casual | Member |
| --- | ---: | ---: |
| Recorded trips | 880,637 | 2,937,367 |
| Share of recorded trips | 23.1% | 76.9% |
| Mean duration | 57.0 minutes | 14.3 minutes |
| Median duration | 25.8 minutes | 9.8 minutes |
| Trips exceeding one hour | 16.52% | 0.42% |
| Share of group trips on weekends | 43.0% | 18.5% |

- Member departures have pronounced morning and evening peaks, including 8 a.m. and 5 p.m. This is consistent with commuting, although trip purpose is not recorded.
- Casual departures have a broader afternoon concentration. Casual trips average about 1.89 times as many per weekend day as per weekday.
- Both groups have their highest monthly trip count in August.

## Data quality and sensitivity

Validation found no duplicate trip IDs across the year, no exact duplicate rows within quarterly files, and no missing or unparseable start or end timestamps. Reported durations were parseable and positive.

However, **1,848 trips exceed 24 hours**, and **103 records** have reported durations differing from timestamp-derived elapsed time by more than one second. These observations warrant investigation; they do not automatically identify invalid trips.

Restricting duration summaries to trips lasting at most 24 hours changes the casual mean from **57.0 to 39.4 minutes** and the member mean from **14.3 to 12.9 minutes**. Medians change little. The analysis therefore emphasizes medians when describing typical trips.

The 24-hour restriction is an exploratory sensitivity check, not a verified data-cleaning rule.

## Proposed next steps for the business

1. **Investigate membership barriers:** survey casual riders about trip purpose, membership awareness, and reasons for not subscribing.
2. **Test membership messaging:** compare a membership-value message with the current experience using a randomized comparison group and a defined conversion window.
3. **Test campaign timing:** use observed casual-trip patterns to propose campaign schedules, measuring incremental conversions and acquisition cost.

These are proposed research activities and experiments, not demonstrated campaign outcomes.

## Limitations

- There are no unique rider identifiers, so individual repeat behavior cannot be established.
- Station endpoints do not reveal the physical route traveled.
- Trip purpose, membership motivations, and marketing responses are unobserved.
- Extreme durations influence means, and timestamp discrepancies require further investigation.
- The analysis is descriptive and does not establish causation.
- Findings describe 2019 and require validation before supporting current decisions.

## Running the notebook

1. Install Python and the required packages:

   ```bash
   python -m pip install "pandas>=2.0" matplotlib jupyter
   ```

2. Place the project notebook in a working folder. Create a `data` subfolder and place all four unzipped quarterly CSVs there.
3. Update the notebook's `files` dictionary to match the exact CSV filenames on your computer. Duplicate-download suffixes such as `(1)` may differ.
4. Set `DATA_DIR = Path("data")` and `OUTPUT_DIR = Path("outputs")`.
5. Open Jupyter Notebook, restart the kernel, and run the cells in order.

The revised workflow creates the `outputs` folder for exported CSV summaries and PNG charts. Final reported values should be checked against the outputs produced by the submitted notebook, particularly if filtering rules change.

## Project materials

- **Notebook:** Python code, analytical explanations, validation, tables, and charts.
- **Report:** Business task, methods, findings, limitations, and recommendations.
- **Outputs:** Exported summaries and visualizations generated by the notebook.

## Skills demonstrated

Data preparation, schema standardization, quality validation, datetime manipulation, descriptive statistics, Boolean filtering, aggregation, data visualization, sensitivity analysis, and communication of findings and limitations.

## Acknowledgments and data use

The case-study scenario comes from the Google Data Analytics Professional Certificate. Historical trip data was made available by Motivate International Inc. for the assignment. Source data remains subject to its original license; consult the download and license references in the project report before redistributing it.
