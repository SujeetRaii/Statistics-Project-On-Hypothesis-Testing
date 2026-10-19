# Statistics Project on Hypothesis Testing

## Overview
This project uses Python to analyze NYC taxi trip records and investigate whether the average fare differs between passengers who pay by card and passengers who pay by cash. The workflow includes data cleaning, exploratory data analysis (EDA), visualizations, and a Welch independent-samples t-test.

## Research Question
**Is there a statistically significant difference in average taxi fare between card-paying and cash-paying customers?**

## Hypotheses
- **Null hypothesis (H₀):** There is no difference in average fare between customers who use cards and customers who use cash.
- **Alternative hypothesis (H₁):** There is a difference in average fare between customers who use cards and customers who use cash.

This is a two-sided test.

## Tools and Libraries
- Python
- Pandas
- NumPy (for numerical/data-analysis work)
- Matplotlib
- Seaborn
- SciPy (`scipy.stats`)
- Statsmodels (Q-Q plot)

## Dataset
The notebook loads a file named `export.csv`, containing taxi trip records. The initial dataset has **1,048,575 rows and 18 columns**. The analysis focuses on:
- `passenger_count`
- `payment_type`
- `fare_amount`
- `trip_distance`
- pickup and drop-off timestamps (used to derive trip duration)

The notebook maps payment type `1` to **Card** and `2` to **Cash**.

## Workflow
1. **Load and inspect data** — review sample rows, dimensions, and data types.
2. **Prepare fields** — parse pickup/drop-off timestamps and calculate trip duration in minutes.
3. **Select relevant columns** — retain passenger count, payment type, fare amount, trip distance, and duration.
4. **Handle missing values** — remove rows missing passenger count or payment type. The notebook reports 2,131 missing values in each of these fields at that stage.
5. **Fix data types** — convert passenger count and payment type to integers and fare amount to a numeric value.
6. **Remove duplicates** — identify and remove 296,736 duplicate rows from the selected five-column dataset.
7. **Filter records** — keep card/cash transactions and passenger counts from 1 to 5, then remove non-positive fare, distance, and duration values.
8. **Treat outliers** — apply the 1.5 × IQR rule to fare amount, trip distance, and duration.
9. **Explore and visualize** — inspect descriptive statistics, compare fare and distance distributions by payment type, plot payment-type proportions, and compare passenger-count percentages.
10. **Test the hypothesis** — compare card and cash fare samples using Welch’s independent-samples t-test (`equal_var=False`).

## Visualizations in the Notebook
- Histogram comparison of fare amounts for card and cash payments
- Histogram comparison of trip distances for card and cash payments
- Pie chart showing payment-type preference
- Stacked horizontal bar chart comparing passenger-count percentages by payment type
- Q-Q plot used to inspect fare distribution

## Statistical Test and Result
The notebook runs Welch’s independent-samples t-test on the cleaned fare samples:

- **Test statistic (t):** 40.652937641916544
- **p-value:** displayed as `0.0` by the notebook

The displayed zero is a numerical representation/underflow for an extremely small p-value, not a claim that the mathematical probability is exactly zero. At a conventional significance level of **α = 0.05**, the p-value is far below the threshold. Therefore, **reject H₀** and conclude that the data provide strong statistical evidence of a difference in average fare between card and cash payments.

The notebook’s descriptive summary before IQR filtering reported average fares of approximately **10.34 for Card** and **9.85 for Cash**. These are intermediate descriptive values, not necessarily the means of the final samples used by the hypothesis test.

## How to Run
1. Place `export.csv` in the same directory as the notebook.
2. Install the required packages:
   ```bash
   pip install pandas numpy matplotlib seaborn scipy statsmodels jupyter
   ```
3. Open and run `stats.ipynb` in Jupyter Notebook or JupyterLab.

## Repository Files
- `stats.ipynb` — analysis notebook
- `export.csv` — input dataset expected by the notebook (not included here)

## Notes and Limitations
- The result shows a statistically significant difference, but statistical significance alone does not establish that the difference is practically large or causal.
- Taxi records can contain extreme or unusual values. The notebook removes non-positive fare, distance, and duration values and then applies IQR-based outlier filtering.
- The reported t-test result is based on the data and processing steps in the notebook. If the input data or cleaning steps change, the result may change.
