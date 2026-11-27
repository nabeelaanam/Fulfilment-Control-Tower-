# Fulfilment-Control-Tower-

# Fulfilment Control Tower — FMCG Distribution OTIF & Shortage Analysis (Jan 2024 – Dec 2025)

## Project Overview
An end-to-end supply chain and fulfilment analytics solution built in **Microsoft Excel (Power Query, Pivot Tables, and Excel Formulas)** to evaluate On-Time In-Full (OTIF) delivery performance, unit fill rates, and financial shortage exposure across a 24-month FMCG distribution dataset. 

The workbook consolidates **24 monthly raw CSV extracts** (50,000 order lines across 25,000 orders, 8 Distribution Centres, and 60 SKUs) into a clean analytical model and executive control tower to pinpoint regional bottlenecks and prioritize high-value shortage lines for operations follow-up.

---

## Business Problem
While aggregate **Unit Fill** appears healthy at **87.7%**, complete **Order OTIF** stands at just **32.2%**. Leadership needed granular visibility into:
1. Why complete order fulfilment lags significantly behind unit-level fill rates.
2. Which Distribution Centres (DCs) and regions drive the highest unit shortages.
3. Monthly service stability and seasonal dips across the 2024–2025 window.
4. Specific high-value unfulfilled order lines requiring immediate operational intervention.

---

## Key KPIs & Headline Findings (Jan 2024 – Dec 2025)

| Metric | Value | Definition / Scope |
| :--- | :--- | :--- |
| **Total Order Lines / Orders** | 50,000 lines / 25,000 orders | Across 60 SKUs, 3 Categories, and 2 Channels (`Online`, `In-Store`) |
| **Eligible Lines / Orders** | 49,435 lines / 24,950 orders | Excludes lines with missing promise dates (`Valid = 0`) and fully cancelled lines |
| **Net Eligible Units** | 5,437,276 units | Ordered quantity net of pre-fulfilment cancellations |
| **Delivered Units** | 4,770,850 units | Total units successfully delivered |
| **Shortage Units** | 666,426 units | Unfulfilled units across eligible lines |
| **Unit Fill Rate** | **87.74%** | `Delivered Units / Eligible Units` |
| **Line OTIF** | **58.06%** | 28,703 of 49,435 eligible lines delivered in full and on/before promise date |
| **Order OTIF** | **32.21%** | 8,037 of 24,950 eligible orders where *every* eligible line passed OTIF |
| **Shortage Exposure** | **₹8.59 Cr** (`₹85,910,580`) | Total INR value of unfulfilled units (`Shortage Qty × UnitPriceINR`) |

### Actionable Insights
* **DC Bottlenecks:** **DC07 (Kolkata DC – East)** and **DC03 (Delhi DC – North)** are the primary underperformers, posting **84.57%** (106,199 short units) and **84.82%** (102,560 short units) unit fill rates respectively—roughly 4 percentage points below the ~88.5–89.2% benchmark maintained by the other six DCs.
* **Service Dip:** Across the 24-month timeline, monthly Unit Fill averaged ~87.7% (peaking at **88.87%** in March 2025) before experiencing a notable trough in **October 2025 (86.30%, 30,576 short units)**.
* **Multi-Line Order Drag:** Because a multi-line order fails Order OTIF if even a single line is late or short, a **58.06%** Line OTIF translates into only **32.21%** complete Order OTIF.

---

## Dataset & Data Model Architecture
* **Source Data:** 24 monthly line-level and delivery CSV files (`Lines_2024_01.csv` to `Lines_2025_12.csv`), ingested and appended via **Power Query**.
* **Dimensions Covered:**
  * **Distribution Centres (8):** `DC01` Mumbai (West), `DC02` Pune (West), `DC03` Delhi (North), `DC04` Jaipur (North), `DC05` Bangalore (South), `DC06` Chennai (South), `DC07` Kolkata (East), `DC08` Patna (East).
  * **Product Categories (3):** Packaged Food, Personal Care, Home Care (60 total products).
  * **Sales Channels (2):** Online, In-Store.
* **Data Quality & Business Rules:**
  * `Valid = 0` (50 lines with missing promise dates) are excluded from service denominators, and their parent orders are excluded from Order OTIF.
  * `NetQty` is derived as `OrderedQty - CancelledQty`; lines with `NetQty > 0` and `Valid = 1` are flagged as `Eligible Line = 1`.
  * `Line OTIF = 1` requires `DeliverQty >= NetQty` AND `Actual Delivery Date <= Expected Delivery Date`.

---

