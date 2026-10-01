# SuperStore Sales Dashboard Project (Interactive Dashboard using Power BI)

## 📌 Project Objective

The goal of this project is to analyze sales performance data from a retail superstore and build a dynamic dashboard using Power BI. The dashboard helps stakeholders understand sales trends, profit distribution, product performance, and regional insights to drive better business decisions.

---

## 📂 Project Files

- **Power BI Dashboard File:** `Retail Supply Chain Dashboard.pbix`
- **Primary Dataset:** 

---

## ❓ Key Questions Addressed

1. What is the total sales, profit, and quantity sold across different regions?
2. Which product categories and sub-categories perform best?
3. Which states are contributing the most to sales and profits?
4. What is the trend of sales and profit over time (monthly/quarterly/YoY)?
5. How do promotional discount thresholds impact profitability and gross margin leakage?
6. Which customer segments and shipping modes deliver the highest operational returns?

---

## 📊 Dashboard Interaction & Architecture

The report is structured into dedicated operational views:

- **Executive View:** High-level KPI cards (Total Sales, Total Profit, Total Quantity, Average Delivery SLA) paired with tile slicers and segment breakdowns.
- **Sales & Profitability Analysis:** Category and sub-category performance matrices highlighting margin compression.
- **Trend & YoY Tracking:** Multi-year monthly progression comparing historical trajectories against prior-year baselines.
- **Root-Cause Tree Decomposition:** Multi-level exploratory paths drilling from business divisions down to regional logistics modes.

### 🔗 Dashboard Snapshot

<img width="935" height="525" alt="image" src="https://github.com/user-attachments/assets/d4895f16-8b80-45b7-aa07-22cc9dee3ea3" />


---

## 🔄 Data Pipeline & Methodology

1. **Data Cleaning & ETL (Power Query):**
   - Ingested transactional records and validated column types across geographic, financial, and temporal entities.
   - Parsed order and shipment dates using invariant locale standards (`MM/DD/YYYY` and `DD/MM/YYYY`).
   - Engineered the calculated column `Delivery Days` using duration differences to track shipping service levels.
   - Handled missing attributes and standardized spatial fields (e.g., postal codes).

2. **Data Modeling & DAX Measures:**
   - Established a dedicated, continuous `Calendar` table with automated monthly sorting logic (`Month Number`).
   - Linked transactional tables to the time dimension using single-directional 1-to-Many (`1:*`) relationships.
   - Formulated dynamic financial measures, including:
     - `Total Sales = SUM('Sample - Superstore'[Sales])`
     - `Total Profit = SUM('Sample - Superstore'[Profit])`
     - `Profit Margin = DIVIDE([Total Profit], [Total Sales], 0)`
     - `Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Calendar'[Date]))`
     - `Profit LY = CALCULATE([Total Profit], SAMEPERIODLASTYEAR('Calendar'[Date]))`

3. **Visual Design & Layout:**
   - Implemented an executive dark theme (`#141836` canvas with `#1E2246` card containers).
   - Applied conditional visual formatting, custom donut charts, horizontal bar rankings, and dark satellite map layers.

---

## 🔍 Key Insights

- **Category Margin Disparity:** **Technology** generates the highest profit margin (~**17.40%**) on high gross revenue ($836K+), whereas **Furniture** operates at a compressed **2.49%** margin despite generating over $741K in sales due to heavy promotional markdown reliance.
- **Direct Loss Drivers:** The sub-categories **Tables** (-$17.7K net loss, -8.56% margin, 26.1% average discount) and **Bookcases** (-$3.5K net loss, 21.1% average discount) account for severe profit leakage, offset by profit engines like **Copiers** (+$25.0K) and **Phones** (+$13.0K).
- **Geographic & State Performance:** **California** and **New York** serve as dominant revenue generators. Regionally, the **West** leads in total profit ($108.4K, 14.94% margin) with controlled discounting (10.9%), whereas the **Central** territory experiences significant erosion (7.92% margin) where nearly **1 in 3 transactions (31.9%)** sells at a loss.
- **Fulfillment & SLAs:** **Standard Class** accounts for approximately 59% of shipment volume with a steady 5-day delivery duration, while **First Class** (2.2 days) and **Same Day** (same-day turnaround) maintain SLAs without diluting shipping margins.
- **Discount Threshold Impact:** Orders with discount rates exceeding **20%** represent over $135K in cumulative gross losses, isolating discounting policies as the primary driver of negative-return sales.

---

## ✅ Final Recommendations

1. **Enforce Category Discount Ceilings:** Implement strict discount governance capping promotional rates below 20% on Furniture lines (specifically Tables and Bookcases) to recover an estimated $22K–$53K in leaked margin.
2. **Capitalize on Technology Lines:** Expand inventory and marketing investment around high-performing sub-categories (Phones, Accessories, Copiers) within top-tier metropolitan territories.
3. **Restructure Central Region Pricing:** Conduct an operational audit of Central territory distribution channels to address the 31.9% loss-making order frequency and align regional margins with the West benchmark.
4. **Leverage Corporate Segment Relationships:** Target Corporate and B2B buyers with loyalty agreements and structured terms rather than arbitrary line-item discounts.
