# 🍨 B.Laban | Commercial & Operational Intelligence Suite

<div align="center">

[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![DAX](https://img.shields.io/badge/DAX-Analysis_Services-00758F?style=for-the-badge)](https://learn.microsoft.com/dax/)
[![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)]()

**Omnichannel Retail Analytics, Delivery Logistics & Inventory Risk Diagnostic**  
*An End-to-End Analytics Workflow Built with Python (Pandas), Star Schema Modeling, and Interactive Power BI*

</div>

---

## 📌 Business Overview

**B.Laban (بـ لبن)** operates a high-volume dessert retail network across Egypt, relying heavily on dynamic fulfillment channels (Delivery, Dine-in, and Takeaway). Managing rapid order throughput while maintaining kitchen efficiency and product availability introduces severe operational bottlenecks.

This project delivers an end-to-end analytical solution designed to transform granular transactional and store logs into actionable intelligence, answering three primary business challenges:
1. **Commercial Throughput & Basket Economics:** Evaluating cross-channel revenue milestones (2.85M EGP across 19K+ orders) and basket expansion via Average Order Value (AOV ~150.23 EGP).
2. **Kitchen Latency & Operational Wastage:** Diagnosing branch fulfillment times (41.8 min network average) against raw ingredient loss (9.3 tons of food waste recorded).
3. **Supply Chain & Stockout Vulnerability:** Mapping localized inventory shortages across core dessert categories (Kunafa, Ice Cream, Basbousa, Crepe) to secure replenishment cycles.

---

## 📊 Executive Performance Dashboard

<p align="center">
  <img src="dashboard_overview.png" alt="B.Laban Operations Dashboard" width="100%" style="border-radius: 8px; box-shadow: 0 8px 24px rgba(0,0,0,0.4);">
</p>

<p align="center">
  <em>Figure 1.0: Real-time Operational Cockpit tracking sales run-rate, channel distribution, SKU rankings, branch service latencies, and category stockout matrices.</em>
</p>

### Key Functional Blocks:
* **Executive KPI Banner:** Immediate visibility into top-line indicators: Total Sales, Order Volume, AOV, Total Units Sold, and Stock Availability Rate.
* **Monthly Revenue Run-Rate:** Dynamic area trend tracking month-over-month fiscal progression and sales volatility.
* **Omnichannel Share:** Segmented visual isolating volume distribution across Delivery, Dine-in, and In-Store channels.
* **Top 10 Revenue Generators:** Granular product hierarchy ranking high-margin and fast-moving SKUs.
* **Branch Operational Efficiency:** Multi-metric benchmark evaluating food waste tonnage against delivery fulfillment latency per location.
* **Inventory Out-of-Stock Risk:** Color-graded contingency matrix identifying critical supply shortages across branches and product families.

---

## 🛠️ Data Pipeline & Architecture

```text
┌───────────────────────┐      ┌──────────────────────────┐      ┌─────────────────────────┐
│   Raw Multi-Source    │ ───► │  Python ETL Engine       │ ───► │  Star Schema Data Model │
│   CSV Store Datasets  │      │  (Pandas Processing)     │      │  (Fact & Dimension Rel) │
└───────────────────────┘      └──────────────────────────┘      └─────────────────────────┘
                                                                              │
                                                                              ▼
                                                                 ┌─────────────────────────┐
                                                                 │  Microsoft Power BI     │
                                                                 │  (DAX & Glassmorphic UI)│
                                                                 └─────────────────────────┘
