# Retail-Sales-Profit-Analytics-Dashboard
Developed an end-to-end Retail Sales Analytics and Forecasting solution using Excel, Python, SQL, Machine Learning, and Power BI. Cleaned and analyzed sales data, identified key business insights, built a Linear Regression sales forecasting model, and created an interactive Power BI dashboard with KPIs and visualizations.

The project follows this workflow:

Excel Raw Data
      ↓
Python + Pandas
      ↓
Data Cleaning & Transformation
      ↓
Cleaned CSV
      ↓
SQLite Database
      ↓
SQL Analysis
      ↓
Simple Sales Forecast
      ↓
Power BI Dashboard

 Tools

- Python
- Pandas
- NumPy
- OpenPyXL
- SQLite / SQL
- Scikit-learn
- Power BI
- Git / GitHub

## Project Structure


retail-sales-profit-project/
│
├── 01_Raw_Data/
│   └── sales.xlsx
│
├── 02_python/
│   ├── data_analytics.py
│   ├── load_to_sql.py
│   ├── run_sql.py
│   └── forecast.py
│
├── 03_Cleaned_Data/
│   └── cleaned_sales.csv
│
├── 04_SQL/
│   ├── retail_analysis.sql
│   └── retail.db
│
├── requirements.txt
├── .gitignore
└── README.md
1. Data Cleaning

data_analytics.py`:

- Reads the Excel dataset.
- Checks shape and column names.
- Checks missing values.
- Checks duplicate rows.
- Removes duplicate rows.
- Calculates `Sales`.
- Calculates `Profit`.
- Calculates `Profit_Margin`.
- Saves `cleaned_sales.csv`.

### Main calculations

python
data["Sales"] = (
    data["Quantity"] * data["Unit_Price"] * (1 - data["Discount"])
)

data["Profit"] = data["Sales"] - data["Cost"]

data["Profit_Margin"] = (
    data["Profit"] / data["Sales"].replace(0, pd.NA)
) * 100

## 2. SQL Database

load_to_sql.py` loads the cleaned CSV into a SQLite database.

The database contains the table:


retail_sales


Run:

```bash
python 02_python/load_to_sql.py
```

## 3. SQL Analysis

`retail_analysis.sql` and `run_sql.py` answer:

- What are total sales?
- Sales by product?
- Sales by region?
- Profit by product?
- Sales by customer?
- Sales by payment mode?

Example:

sql
SELECT
    Product,
    SUM(Sales) AS Total_Sales
FROM retail_sales
GROUP BY Product
ORDER BY Total_Sales DESC;


## 4. Simple Sales Forecast

forecast.py` uses `LinearRegression` from Scikit-learn to demonstrate a basic sales forecast.

Important: this is a **simple learning/portfolio forecast**, not a production forecasting model. With a very small dataset, forecast results should not be treated as business predictions.

## 5. Power BI Dashboard

The cleaned CSV is imported into Power BI.

### KPI Cards

- Total Sales → ₹232,900
- Total Profit → ₹27,400
- Total Quantity → 15

### Visuals

**Sales by Product**
```text
X-axis → Product
Y-axis → Sales
```

**Sales by Region**
```text
X-axis → Region
Y-axis → Sales
```

**Profit by Product**
```text
X-axis → Product
Y-axis → Profit
```

**Sales by Payment Mode**
```text
X-axis → Payment_Mode
Y-axis → Sales
```

**Sales by Customer**
```text
X-axis → Customer_Name
Y-axis → Sales
```

### Slicers

- Region
- Product

The slicers make the dashboard interactive.

## 6. Results from the 5-row sample used in the project

```text
Total Sales     = ₹232,900
Total Profit    = ₹27,400
Total Quantity  = 15
```

### Sales by Product

```text
Laptop  = ₹145,000
Mobile  = ₹54,000
Chair   = ₹22,500
Shoes   = ₹11,400
```

### Sales by Region

```text
South = ₹145,000
North = ₹54,000
West  = ₹22,500
East  = ₹11,400
```

### Profit by Product

```text
Laptop = ₹17,500
Mobile = ₹6,000
Chair  = ₹2,500
Shoes  = ₹1,400
```

### Sales by Payment Mode

```text
UPI  = ₹117,500
Card = ₹104,000
Cash = ₹11,400
```

## 7. Business Insights

Based on this sample:

- Laptop has the highest sales.
- South has the highest sales.
- UPI has the highest sales among payment modes.
- Laptop has the highest total profit.

These findings are specific to the small sample dataset and should not be generalized to a larger business without more data.

## 8. How to Run

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

Put the Excel file here:

```text
01_Raw_Data/sales.xlsx
```

Then run:

```bash
python 02_python/data_analytics.py
python 02_python/load_to_sql.py
python 02_python/run_sql.py
python 02_python/forecast.py
```

Then open Power BI and import:

```text
03_Cleaned_Data/cleaned_sales.csv
```

Build the dashboard using the cards, charts, and slicers described above.


