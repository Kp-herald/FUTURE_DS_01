Markdown
# Superstore Retail Sales & Profitability Analytics Dashboard

## 📌 Project Overview
An end-to-end data analytics and business intelligence project evaluating multi-year retail transactional performance across 5,000+ distinct orders ($2.30M gross revenue, $286.4K net profit). 

The primary objective is to analyze revenue trends over time, identify high-revenue and top-selling products, evaluate category and regional profitability, and formulate data-driven strategic recommendations to optimize enterprise profit margins.

---

## 🛠️ Tech Stack & Methodology
- **Analytics & BI Platform:** Microsoft Power BI Desktop
- **Data Transformation:** Power Query (data cleaning, type casting, schema validation)
- **Data Modeling:** Star Schema architecture with an independent, dynamic `Calendar` dimension table
- **Calculations:** DAX (Data Analysis Expressions) for dynamic business metrics and KPI tracking

---

## 📊 Dashboard Preview
![Dashboard Preview](Dashboard_overview.png)

### Dashboard Structure:
1. **Executive KPI Scorecard:** `Total Orders (5,009)`, `Total Profit ($286.4K)`, `Total Sales ($2.30M)`, and `Net Profit Margin (12.47%)`.
2. **Top 10 Products by Revenue (Horizontal Bar Chart):** Ranks the top revenue-generating SKUs, led by enterprise printing and copying systems.
3. **Monthly Sales & Profit Trend (Line & Clustered Column Chart):** Tracks monthly volume and profitability cycles to evaluate seasonal performance.
4. **Profitability by Sub-Category (Conditional Bar Chart):** Visually differentiates profit drivers (Green) from chronic loss leaders (Red).
5. **Profits & Sales by Region (Clustered Bar Chart):** Evaluates geographic revenue volume vs. profit conversion across West, East, South, and Central territories.
6. **Interactive Slicers:** Dynamic filters for `Year`, `Region`, and `Segment` for ad-hoc scenario analysis.

---

## 📐 Key DAX Measures

```dax
-- Dedicated Calendar Dimension Table
Calendar = 
ADDCOLUMNS (
    CALENDAR ( MIN ( 'Sample - Superstore'[Order Date] ), MAX ( 'Sample - Superstore'[Order Date] ) ),
    "Year", YEAR ( [Date] ),
    "Month", FORMAT ( [Date], "mmm" ),
    "Month Number", MONTH ( [Date] ),
    "Year-Month", FORMAT ( [Date], "yyyy-mm" ),
    "Quarter", "Q" & FORMAT ( [Date], "q" )
)

-- Core Financial Measures
Total Sales = SUM ( 'Sample - Superstore'[Sales] )
Total Profit = SUM ( 'Sample - Superstore'[Profit] )
Profit Margin = DIVIDE ( [Total Profit], [Total Sales], 0 )
Total Orders = DISTINCTCOUNT ( 'Sample - Superstore'[Order ID] )
🔍 Key Analytical Findings
1. Revenue Trends & Seasonality
Q4 Annual Surge: Sales and transaction volume consistently peak between September and December, with November ($352K) and December ($325K) generating peak annual volume due to corporate year-end procurement and holiday demand.  
PDF

Q1 Contraction: January ($94K) and February ($59K) represent recurring demand troughs, dropping by over 55% compared to Q4 peaks.  
PDF

March Procurement Spike: A reliable spring surge occurs consistently every March ($205K sales, $30K profit).  
PDF

2. Top-Selling & High-Value Products
Top Revenue SKU: Canon imageCLASS 2200 Advanced Copier generates $61,599.82 in total revenue and serves as the single largest profit driver[cite: 3].

High-Value Office Systems: Fellowes PB500 Electric Punch Binding Machine ($27.5K) and Cisco TelePresence System EX90 ($22.6K) drive top-line volume[cite: 3].

3. Category & Regional Diagnostics
Profit Drivers: Technology (17.39% margin) and Office Supplies (17.03% margin) serve as the primary profit engines, led by Copiers (37.20% margin) and Paper (43.39% margin)[cite: 3].

Profit Leaks: The Furniture category suffers severe margin compression (2.49% net margin) caused by heavy net losses in Tables (-$17,725) and Bookcases (-$3,473) due to excessive promotional discounting (>20–40%)[cite: 3].

Regional Disparities: The West (14.94% margin) and East (13.48% margin) lead the company in profitability, while the Central region lags at 7.92% margin due to aggressive price discounting in key metro markets[cite: 3].

💡 Strategic Business Recommendations
Implement Hard Discount Caps on Furniture: Enforce a hard system constraint capping maximum allowable discounts on Furniture at 15% to eliminate negative-margin orders, recovering an estimated $15,000–$18,000 in annual bottom-line profit[cite: 3].

Deploy High-Margin Product Bundling: Bundle high-margin hardware (Copiers at 37.2% margin) with recurring high-margin office consumables (Paper at 43.4% margin) through multi-quarter corporate contracts[cite: 3].

Restructure Regional Sales Incentives: Transition Central territory sales commission models from Gross Revenue Volume to Gross Margin Realized, disincentivizing excessive price slashing[cite: 3].

Counter Q1 Seasonal Slumps: Introduce early-bird annual contract renewals in late Q4 with scheduled Q1 replenishment delivery rebates to smooth annual revenue volatility[cite: 3].

📁 Repository Structure
├── Business_Sales_Profitability_Report.pdf  # Comprehensive 3-page executive advisory report
├── Dashboard_overview.png                  # High-resolution dashboard overview snapshot
├── Sample - Superstore.csv                 # Raw transactional dataset (CSV)
├── Super Store sales.pbix                  # Full interactive Power BI Desktop model
└── README.md                               # Project documentation & analysis brief
