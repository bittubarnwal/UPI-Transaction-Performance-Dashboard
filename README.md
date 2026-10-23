# UPI Transaction Performance Dashboard

A beginner-level Power BI project using a purple-and-white theme, standard charts, slicers, Power Query, and basic DAX.

## Dataset

Source: [UPI Transactions 2024 Dataset by skullagos5246 on Kaggle](https://www.kaggle.com/datasets/skullagos5246/upi-transactions-2024-dataset).

This dataset is synthetic and is used for educational and portfolio purposes; it is not actual bank data.

The original CSV contains 250,000 transactions and 17 columns. Dates range from 1 January to 30 December 2024; 31 December is absent.

The report compares sender banks, not branches. Onboarding analysis is outside this dataset because it has no application or processing-time fields.

## How to use

Open `UPI Transaction Dashboard.pbix` in Power BI Desktop. Use the Month, Sender bank, Transaction type, and Sender state dropdowns to filter the page. Clear each slicer to return to all transactions. Selecting chart categories filters related visuals; click the selected category again to clear it.

The report contains imported data. The CSV is stored beside the PBIX in this repository. Before refreshing, open Transform data > Edit parameters and update `DataFile` to the full path of `upi_transactions_2024.csv`, then refresh. The saved PBIX still uses its original source path until you update this parameter.

## Measures

- Total transactions: number of transaction rows after duplicate removal.
- Attempted value: sum of all amounts, including failed attempts; displayed in crore (1 crore = 10 million INR).
- Success rate: successful transactions / total transactions.
- Failure rate: failed transactions / total transactions.
- Average amount: average attempted transaction amount.

Failed amounts are not proven financial losses. Fraud flags are separate from transaction failure status and are not used to calculate failure rates.

## Preparation

Power Query promotes headers, gives columns readable names, sets date and number types, trims selected text fields, standardizes status, removes duplicate transaction IDs, and derives a date, month label, and month number. Month is sorted by month number.

The downloaded file has no missing values and no duplicate transaction IDs. The cleaning steps are preventive; no missing records or duplicates were invented for this project.

The single-table model is intentional for a first project. Basic measures use COUNTROWS, SUM, AVERAGE, CALCULATE, and DIVIDE. The DAX measures and Power Query steps are stored inside the PBIX file.

## Results with all filters cleared

| KPI | Value |
|---|---:|
| Transactions | 250,000 |
| Successful | 237,624 |
| Failed | 12,376 |
| Success rate | 95.0496% |
| Failure rate | 4.9504% |
| Attempted value | INR 327,939,009 |
| Successful value | INR 311,181,812 |

SBI has the largest transaction count in this sample: 62,693 (25.08%). Yes Bank has the highest observed failure rate, 5.10%, and HDFC has the lowest, 4.82%. The gap is only about 0.28 percentage points. These synthetic differences do not establish real bank quality or failure causes.

Suggested next steps for a real operations team would be to investigate failure reason codes, monitor rates together with transaction counts, and compare multiple periods before deciding which bank or device needs attention. This dataset cannot establish root causes.

## Validation

The report was refreshed, saved as a PBIX, and reopened in Power BI Desktop. The all-data KPI cards match the source totals above. Selecting January returned 21,221 transactions and 1,012 failures, matching a separate CSV calculation. All filters were cleared before saving the final dashboard.


## Repository files

- [UPI Transaction Dashboard.pbix](UPI%20Transaction%20Dashboard.pbix): the Power BI report, including imported data and calculations.
- [upi_transactions_2024.csv](upi_transactions_2024.csv): the complete source dataset.
- README.md: project overview, metric definitions, results, and opening instructions.

## Tools used

Power BI Desktop, Power Query, and DAX. Excel was used for supporting checks during development.

## View the report

Download the PBIX file and open it in Power BI Desktop to explore the interactive visuals. The local source path only needs updating if you want to refresh the data on another computer.
