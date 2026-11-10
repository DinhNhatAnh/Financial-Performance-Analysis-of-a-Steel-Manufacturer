# Financial Performance Analysis: ABC Manufacturing (Steel), FY2024–FY2025

Quarterly financial KPI analysis of a steel manufacturer, built in Python from 8 source tables. The project covers profitability, liquidity, leverage, cash flow, working capital and budget variance, and includes a data-validation step that checks whether the three financial statements reconcile.

> **Note:** The dataset is simulated for this case study. It does not represent any real company, and the findings should not be read as real-world business results.

## Business questions

1. How fast are revenue and profit growing, and are margins improving?
2. Does the company have enough liquidity, and is its debt level safe?
3. Does profit convert into cash actually collected?
4. How far do actual results deviate from the budget each quarter?

## Key findings (Q1/2024 → Q4/2025)

| Area | Finding |
|---|---|
| Profitability | Net profit grew **116%** vs. revenue **52%**. Net margin expanded **7.8 pp** (18.4% → 26.2%); about two-thirds of the operating-margin gain came from a lower COGS ratio (60.0% → 54.4%). |
| Working capital | Cash conversion cycle shortened by **13.2 days** (28.8 → 15.6), almost entirely from lower inventory days (DIO −12.2). |
| Liquidity & leverage | Current ratio 2.20x → **2.62x**; debt-to-equity 0.67x → **0.36x**; interest coverage 22.9x → 63.3x. Idle cash is building up. |
| Cash flow | FCF doubled (160K → 320K USD), but the cash conversion ratio (OCF / net profit) fell from 1.09x to **0.90x**. |
| Budget | Net profit moved from −6.0% below plan to **+17.8%** above plan, so the profit budget has not tracked margin expansion. |

## Data

8 CSV tables (4 fact, 4 dimension), 8 quarters (Q1/2024–Q4/2025):

| Type | Tables |
|---|---|
| Fact | `fact_income_statement.csv`, `fact_balance_sheet.csv`, `fact_cashflow.csv`, `fact_budget.csv` |
| Dimension | `dim_company.csv`, `dim_date.csv`, `dim_account.csv`, `dim_department.csv` |

## Method

1. **Load and merge:** read the 8 tables with pandas and merge them on `date_id` into a quarterly master table.
2. **Compute KPIs:** 50+ metrics in 8 groups: P&L waterfall, margins, profitability (ROA/ROE), liquidity, leverage, cash flow, working capital, budget variance.
3. **Validate:** reconcile the balance sheet, cash flow statement and equity; flag inconsistencies.
4. **Visualize and interpret:** Matplotlib charts for each KPI group, with findings and strategic recommendations.

## Known data limitations

- `Other_Assets_Unreconciled` is a balancing plug flagged "pending source verification" (85K USD, ~4.8% of total assets by Q1/2025).
- Cumulative net cash flow for Q2/2024–Q4/2025 is +1,535K USD, but the cash balance rose only +125K USD.
- Annualized ROA/ROE (quarterly × 4) reach 98% and 148%, which is unrealistic, so they are not used as a basis for conclusions.
- Only 8 quarters of data, and a ~26% net margin is far above typical steel-industry levels.

## Recommendations (summary)

- **Protect margins:** break down the drivers of lower COGS, stress-test margins, and set alert thresholds for COGS and OPEX ratios.
- **Use surplus cash by plan:** set a target liquidity level and allocate the excess to investment, dividends or high-cost debt repayment.
- **Improve cash flow quality:** bring the cash conversion ratio back above 1.0x and keep safety stock instead of squeezing inventory further.
- **Budget closer to reality:** base the profit budget on the latest actual margin and track variance every quarter.

## Repository structure

```
.
├── data/                          # 8 source CSV files
├── Finance_Analysis.ipynb         # full analysis notebook
├── kpi_summary.csv                # exported KPI table (one row per quarter)
├── Portfolio_Financial_Analysis_EN.pptx   # presentation summarizing the project
└── README.md
```

## How to run

```bash
pip install pandas numpy matplotlib jupyter
jupyter notebook Finance_Analysis.ipynb
```

Place the 8 CSV files where the notebook's `read_csv` calls expect them (update the paths in the setup cell if you keep them in `data/`).

## Tech stack

Python · pandas · NumPy · Matplotlib · Jupyter Notebook
