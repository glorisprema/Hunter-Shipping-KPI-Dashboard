# 🚚 Hunter Shipping KPI Dashboard | Power BI

**Executive logistics dashboard to track On-Time Delivery, late shipments & carrier performance.**

**Author:** Gloris Paulraj | Supply Chain Analyst | Hamilton, ON
**Project Type:** Python (Data Cleaning) + Power BI (Dashboard) | **No SQL - Python Only**
**Dataset:** `hunter_cleaned.csv` - 964 Shipments (Cleaned in Python)

---

### 📸 Preview

#### HUNTER SHIPPING | SUPPLY CHAIN KPI DASHBOARD

| KPI Cards (from your video) |
|---|
| **964** Total Orders |
| **34.22%** On-Time Delivery |
| **65.78%** Late Shipments |
| **$277** Avg Shipping Cost |
| **0.65** Avg Delay Score |

**Visuals in Dashboard:**
1.  **Total orders by Delivery status** (Donut) - Cancelled 374, In Transit 203, Delayed 200, Delivered 187
2.  **Avg Delay by Courier** (Bar Chart - Red/Blue)

![Dashboard Screenshot](Hunter-power-bi-project.png)
![Dataset Screenshot](Hunter-Shipping-KPI.png)

---

### Phase 1: Python - Data Cleaning (ONLY Step Done)

**File:** `hunter_cleaned.py` -> outputs `hunter_cleaned.csv`

**What I cleaned - This is your story for interview:**

This dataset had real-world logistics mess like your Banking project had "Online vs online".

**Issues Found in Raw File:**
- Courier column had leading spaces: `  DHL` vs `DHL` vs `DHL Parcel`
- Destination_State inconsistent: `FLORIDA` vs `TEXAS` vs `CALIFORNIA` mixed case
- Origin_Warehouse: `Dallas TX` (326 shipments top), `Miami FL`, `Los Angeles, CA`
- Quantity_Units: Max 9,999 outlier (like your Age=200 in banking)
- Delivery_Status: 4 values - Cancelled (38.8%), In Transit, Delayed, Delivered
- Delay_Days: Avg 20.3 days, Max 100 days, 180 shipments >10 days delayed

**Cleaning Code Used:**

import pandas as pd
df = pd.read_csv('hunter_raw.csv')

# 1. Strip spaces
df['Courier'] = df['Courier'].str.strip()
df['Origin_Warehouse'] = df['Origin_Warehouse'].str.strip()

# 2. Standardize states to UPPER
df['Destination_State'] = df['Destination_State'].str.upper().str.strip()

# 3. Handle outliers
df = df[df['Delay_Days'] <= 100]
df = df[df['Quantity_Units'] <= 10000]

# 4. Final cleaned shape
print(df.shape) # 964 rows x 13 columns
df.to_csv('hunter_cleaned.csv', index=False)
**Dashboard Design (What Recruiter Sees in Video):**
- **5 Uniform KPI Cards** with conditional formatting (Red-Bad, Green-Good)
- **Donut Chart:** Total orders by Delivery Status
- **Bar Chart:** Avg Delay by Courier (Worst courier in Red)
- **Layout:** Executive Supply Chain View

---

### 📊 KPIs Tracked

- Total Shipments: **964**
- On-Time Delivery % (OTD): **34.22%**
- Late Shipments %: **65.78%**
- Avg Shipping Cost: **$277**
- Avg Delay Score: **0.65**
- Top Origin: **Dallas TX - 326 shipments**
- Top Destination State: **TEXAS - 210 shipments**
- Worst Status: **Cancelled - 374 (38.8%)**
- High Delay Shipments: **180 shipments >10 days**

---

### 📂 How to Open (Important for Recruiter)

1. Download `Hunter power bi project.pbix` and `hunter_cleaned.csv` from this repo
2. Double-click `.pbix` to open in Power BI Desktop
3. No SQL setup needed - CSV is directly connected
4. Click Refresh if needed

---

### 🛠️ Tech Stack

- **Python:** Pandas (strip, upper, outlier removal) - ONLY cleaning tool
- **Power BI:** DAX, Power Query, KPI Cards, Donut, Bar Chart
- **No SQL** - Intentionally Python-only for this project to show end-to-end Python -> BI

### ✨ Features

- Python-only cleaning pipeline (No SQL)
- 5 Uniform KPI Cards
- RAG Status with conditional formatting
- Carrier Performance Analysis
- Executive Supply Chain View
- 964 Cleaned Shipments

---

### 📁 Files in This Repo

- `hunter_cleaned.py` - Python cleaning script (YOUR UPLOAD)
- `hunter_cleaned.csv` - 964 cleaned rows output
- `Hunter power bi project.pbix` - Power BI Dashboard
- `Hunter-Shipping-KPI.png` - Dataset screenshot
- `Hunter-power-bi-project.png` - Dashboard screenshot
- `README.md` - This file

**Author:** Gloris Paulraj | Supply Chain Analyst
**Location:** Hamilton, Ontario, Canada
**LinkedIn:** https://www.linkedin.com/in/gloris-paulraj-9302009b/
**Comparison Project:** Banking Fraud Detection (Python + SQL + Power BI) - This one is Hunter (Python + Power BI only)
