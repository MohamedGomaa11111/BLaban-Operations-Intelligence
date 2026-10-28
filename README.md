<div align="center">

# 🍨 B.LABAN | Commercial & Operational Intelligence Suite
### Enterprise Retail Analytics, Kitchen Logistics & Supply Chain Resilience
**End-to-End Business Intelligence Solution Engineered with Python, SQL, Star Schema & Power BI**

---

[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org/)
[![SQL Server](https://img.shields.io/badge/T--SQL-CC292B?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)](https://www.microsoft.com/sql-server)
[![DAX](https://img.shields.io/badge/DAX-Analysis_Services-0078D4?style=for-the-badge)](https://learn.microsoft.com/dax/)
[![Status](https://img.shields.io/badge/Deployment-Production_Ready-success?style=for-the-badge)]()

<br />

<!-- DASHBOARD HERO BANNER (Direct Rendering) -->
<a href="#-executive-dashboard-showcase">
  <img src="dashboard_overview.png" alt="B.Laban Executive Dashboard Overview" width="100%" style="border-radius: 12px; box-shadow: 0 10px 30px rgba(0,0,0,0.5); border: 1.5px solid #203a43;" />
</a>

<br />

**[ 📊 Live Demo Overview ](#-executive-dashboard-showcase)** • **[ 🧠 Data Architecture ](#-data-architecture--star-schema)** • **[ 💡 Business Insights ](#-key-business-insights)** • **[ 🛠️ Setup Guide ](#-quick-start)**

---

</div>

## 📌 Executive Abstract

**B.Laban (بـ لبن)** is Egypt’s hyper-growth quick-service dessert powerhouse. Operating across dozens of high-traffic branches with an omnichannel sales footprint (*Delivery, Dine-in, Takeaway*), the organization faces complex operational dynamics: surging evening order bursts, perishability-constrained inventory, and kitchen dispatch bottlenecks.

This project delivers an **Executive-Grade Analytics Cockpit** built on a normalized Star Schema architecture, surfacing actionable telemetry on **2.85M EGP** in top-line revenue, tracking kitchen food waste (**9.3 tons**), and exposing multi-branch stock-out vulnerabilities before customer churn occurs.

---

## 📊 Executive Dashboard Showcase

<div align="center">
  <img src="dashboard_overview.png" alt="B.Laban Performance & Operations Cockpit" width="100%" />
  <p><em>Figure 1.0: Real-time Operational Cockpit displaying Run-Rate trajectory, Channel Split, Product Rankings, Branch Latencies, and Stock-out Matrices.</em></p>
</div>

### Core Visual Functional Blocks
* **Executive KPI Command Bar:** Instant readouts on *Gross Sales, Total Orders, Average Order Value (AOV), Total Items Sold*, and *Stock Availability Rate*.
* **Monthly Revenue Run-Rate (Area Trend):** Dynamic smoothing tracking monthly financial performance against target milestones.
* **Omnichannel Order Mix (Donut Matrix):** Granular order volume segmentation across Delivery hubs, Dine-in, and In-Store Takeaway.
* **Top 10 Revenue Generators (Bar Hierarchy):** Clear rank visibility identifying flagship product drivers (Large Mixed Box, Mango/Nutella Kunafa, Koshery series).
* **Branch Operational Efficiency (Matrix Grid):** Dual-metric diagnostic pairing physical kitchen waste ($kg$) with governorate dispatch latencies ($mins$).
* **Inventory Out-of-Stock Risk (Heatmap):** Category-level risk index across Kunafa, Basbousa, Crepe, Ice Cream, and Layer lines.

---

## 📈 Key Performance Indicators (KPIs)

| Metric | Measured Value | Operational Meaning & Decision Impact |
| :--- | :---: | :--- |
| **Total Revenue** | **2.85M EGP** | Benchmark performance captured across core regional dessert hubs. |
| **Total Orders** | **19,000+** | High-velocity order throughput requiring optimized dispatch sequencing. |
| **Average Order Value (AOV)** | **150.23 EGP** | ~2.58 items per basket; strong cross-sell performance on signature toppings. |
| **Total Items Sold** | **49,000 units** | Volume throughput across flagship pastry and dairy preparations. |
| **Stock Availability Rate** | **82.1%** | **17.9% stock-out exposure rate**, identifying urgent replenishment triggers. |
| **Cumulative Kitchen Waste** | **9,299.29 kg** | Pinpoints preparation overages requiring tighter daily batch formulas. |
| **Average Delivery Speed** | **41.8 min** | Highlights city centers requiring geo-zone route optimization. |

---

## 🧠 Data Architecture & Star Schema

The project ingests multi-table transactional streams, cleanses anomalies via Python, and models them into an optimized dimensional model to ensure sub-second report interactivity:

```
                      ┌─────────────────────────┐
                      │      Dim_Branches       │
                      ├─────────────────────────┤
                      │ BranchID (PK)           │
                      │ BranchName              │
                      │ Governorate             │
                      └────────────┬────────────┘
                                   │ 1
                                   │
                                   │ *
┌─────────────────────────┐   ┌────┴────────────────────────┐   ┌─────────────────────────┐
│        Dim_Date         │   │  Cleaned_DailyBranchPerf    │   │      Dim_Products       │
├─────────────────────────┤   ├─────────────────────────────┤   ├─────────────────────────┤
│ Date (PK)               │1  │ BranchID (FK)               │  *│ ProductID (PK)          │
│ Year / Month / Day      ├───┤ Date (FK)                   ├───┤ ProductName             │
│ DayOfWeek / WeekEnd     │ * │ FoodWaste_Kg                │ 1 │ Category                │
└─────────────────────────┘   │ AvgDelivery_Min             │   │ UnitPrice               │
                              └─────────────────────────────┘   └────────────┬────────────┘
                                                                             │ 1
                                                                             │
                                                                             │ *
┌─────────────────────────┐   ┌─────────────────────────────┐   ┌────────────┴────────────┐
│     Cleaned_Orders      │ 1 │     Cleaned_OrderItems      │   │  Cleaned_ProductAvail   │
├─────────────────────────┤───┤─────────────────────────────┤   ├─────────────────────────┤
│ OrderID (PK)            │ * │ OrderItemID (PK)            │   │ BranchID (FK)           │
│ OrderDate (FK)          │   │ OrderID (FK)                │   │ Date (FK)               │
│ OrderChannel            │   │ ProductID (FK)              │   │ CategoryID              │
│ TotalAmount             │   │ Quantity, UnitPrice         │   │ OutOfStockCount         │
└─────────────────────────┘   └─────────────────────────────┘   └─────────────────────────┘
```

---

## 📐 Advanced DAX Calculations (Sample)

### 1. Stock Availability Rate %
```dax
Stock Availability Rate % = 
VAR _TotalIncidents = SUM('Cleaned_ProductAvailability'[OutOfStockCount])
VAR _TotalObservations = COUNTROWS('Cleaned_ProductAvailability')
RETURN
IF(
    _TotalObservations > 0,
    1 - DIVIDE(_TotalIncidents, _TotalObservations, 0),
    1
)
```

### 2. Weighted Average Delivery Latency
```dax
Weighted Avg Delivery Min = 
DIVIDE(
    SUMX('Cleaned_DailyBranchPerformance', 'Cleaned_DailyBranchPerformance'[AvgDeliveryMinutes] * 'Cleaned_DailyBranchPerformance'[TotalOrdersCompleted]),
    SUM('Cleaned_DailyBranchPerformance'[TotalOrdersCompleted]),
    BLANK()
)
```

---

## 💡 Key Business Insights

1. **Category Bottlenecks in Kunafa & Crepe:**
   * Kunafa lines experienced over **86 recorded stock-out anomalies**, predominantly during post-8:00 PM evening order peaks.
   * *Prescription:* Shift preparation shifts 90 minutes earlier in Central Cairo & Alexandria kitchens.
2. **Kitchen Waste Dispersion:**
   * **October 6** and **Al-Tagamoa Al-Khames** branches registered the highest waste volumes (>600 kg each).
   * *Prescription:* Implement algorithmic batch forecasting to adjust daily base cream stock based on local weekday patterns.
3. **Channel Performance:**
   * Takeaway and Delivery account for over **70% of total revenue**, confirming B.Laban as an off-premise-first retail concept.

---

## 🗂️ Clean Repository Organization

```text
BLaban-Operations-Intelligence/
│
├── data/
│   ├── Cleaned_DailyBranchPerformance.csv  # Branch logistics, delivery & waste telemetry
│   ├── Cleaned_OrderItems.csv              # Granular order lines & quantities
│   ├── Cleaned_Orders.csv                  # Transaction-level orders and channel splits
│   └── Cleaned_ProductAvailability.csv     # Daily stock availability & out-of-stock logs
│
├── scripts/
│   └── data_cleaning.py                    # Complete automated Python ETL cleansing script
│
├── BLaban_Executive_Dashboard.pbix          # Interactive single-file Power BI Dashboard
├── dashboard_overview.png                  # High-resolution dashboard screenshot
└── README.md                               # Executive documentation & showcase
```

---

## 🚀 Quick Start

1. **Clone the Repo:**
   ```bash
   git clone https://github.com/MohamedGomaa11111/BLaban-Operations-Intelligence.git
   cd BLaban-Operations-Intelligence
   ```

2. **Run ETL Pipeline (Optional):**
   ```bash
   python scripts/data_cleaning.py
   ```

3. **Open the Dashboard:**
   * Launch `BLaban_Executive_Dashboard.pbix` in **Power BI Desktop**.
   * Interact with visual cross-filtering and test page navigation with `Ctrl + Click`.

---

## 👨‍💻 Author & Contact

**Mohamed Gomaa**  
*Business Intelligence Specialist & Data Analyst*  
* Specialized in ETL Automation, Dimensional Modeling & Executive Dashboard Architecture.

* **GitHub:** [@MohamedGomaa11111](https://github.com/MohamedGomaa11111)  
* **Portfolio:** [MohamedGomaa11111.github.io](https://MohamedGomaa11111.github.io/portfolio)  
* **LinkedIn:** [Mohamed Gomaa](https://www.linkedin.com/in/)

---
<div align="center">
  <sub>Developed for Enterprise Analytics Excellence • B.Laban Suite 2026</sub>
</div>