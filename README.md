# Swiggy Sales Analytics Dashboard

A comprehensive data analytics project designed to extract actionable business insights from Swiggy's sales data. This project processes raw transaction data using Python, `pandas`, and `python-calamine` to build critical Key Performance Indicators (KPIs) and satisfy standard Business Requirement Documents (BRD).

---

## 📊 Core Business KPIs Developed

The data pipeline extracts five high-level business metrics to track absolute platform health and financial performance:

* **Total Sales (₹):** Measures overall revenue generated from food orders to track top-line growth.
* **Average Rating:** Calculates the mean customer satisfaction scores across all active restaurant transactions.
* **Average Order Value (AOV) (₹):** Tracks the average revenue generated per unique order (\(Total\ Sales \div Total\ Orders\)).
* **Ratings Count:** Measures the total volume of customer reviews to gauge user feedback density.
* **Total Orders:** Counts the total number of food orders processed across the platform.

---

## 🚀 Key Performance Indicators & Charts Included

The analytical engine processes data to satisfy the following Business Requirement Document (BRD) dashboard visualization layers:

* **Monthly Sales Trend:** Evaluates how total sales fluctuate month over month to observe seasonal trends.
* **Daily Sales Trend:** Highlights order and revenue variations across specific days of the week.
* **Total Sales by Food Type:** Compares revenue contributions between **Veg** and **Non-Veg** cuisine types.
* **Total Sales by State:** Aggregates state-wise revenue distribution for spatial/geographic mapping.
* **Quarterly Performance Summary:** Consolidates Sales, Ratings, and Order Volumes grouped by financial Quarter.
* **Top 5 Cities by Sales:** Pinpoints the top-performing urban centers driving maximum revenue.
* **Weekly Trend Analysis:** Monitors week-to-week revenue volatility to identify core peak operational periods.

---

## 🛠️ Tech Stack & Dependencies

* **Python 3.x** - Core programming runtime environment.
* **Pandas** - Heavy data manipulation, feature extraction, vector sorting, and group aggregations.
* **python-calamine** - An ultra-fast, Rust-backed Excel reader engine used to extract vast transaction datasets smoothly out of binary `.xls/xlsx/xlsb` formats.

### Installation

```bash
pip install pandas python-calamine
```

---

## 📁 Core Data Pipelines (Pandas Architecture)

Below are the computational paradigms used in the source notebooks to extract the business metrics:

### 1. High-Level KPI Calculation
```python
# Calculating the 5 Core Business KPIs
total_sales = df['Sales'].sum()
average_rating = df['Rating'].mean()
total_orders = df['OrderID'].count()

# Business logic for AOV and Total Ratings
average_order_value = total_sales / total_orders
ratings_count = df['Rating'].notna().sum()
```

### 2. Quarterly Performance Aggregation
Utilizes optimized grouping logic bypassing multi-index restructuring for seamless downstream visualization processing.
```python
quarterly_summary = df.groupby('Quarter', as_index=False).agg(
    Total_Sales=('Sales', 'sum'),
    Average_Rating=('Rating', 'mean'),
    Total_Orders=('OrderID', 'count')
)
```

### 3. Geographic & City Rankings
Extracting top revenue nodes using vector-based sorting.
```python
top_5_cities = df.groupby('City', as_index=False)['Sales'].sum() \
                 .sort_values(by='Sales', ascending=False) \
                 .head(5)
```

---

## 📈 Insights Obtained

1. **Dietary Demographics:** Clear visualization breakdown of consumer spending habits across Veg vs Non-Veg menu options.
2. **Temporal Volatility:** Structural identification of peak operational days versus seasonal quarterly variations to assist logistics and vendor optimization.
3. **Regional Hotspots:** Geolocation profiling identifying specific states and top 5 cities carrying the highest density of Gross Merchandise Value (GMV).
