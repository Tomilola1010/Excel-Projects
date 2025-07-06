# 🧹 Data Cleaning Documentation using Power Query in Excel

**Author**: Ayelangbe Tomilola  
🕒 7 min read · 📅 June 15, 2025  

---

## 📌 Introduction

**Data is everywhere, but clean data? That’s rare.**

Whether you're an analyst, researcher, or just someone trying to understand business data, you’ve likely encountered messy Excel files filled with blanks, errors, and formatting inconsistencies.

**Enter Power Query** — a powerful transformation tool built into Excel. This guide walks through a realistic **data cleaning workflow**, from importing messy data to formatting it for clean analysis — all with **zero code**.

---

## 🛠 Tools Needed

- **Microsoft Excel (latest version)**
- **Power Query Editor** (built into Excel)
- Sample file: `Data_Cleaning_Start.xlsx`

---

## 🎯 Objective

To **identify errors** and **clean data** for accurate, readable, and analysis-ready results.

---

## 📄 Overview of the Work

**Raw Dataset:** `Data_Cleaning_Start.xlsx`

### Issues Noticed:
- `#DIV/0!` errors in *Profit Margin*  
- Inconsistent casing in *Client*, *Department*, *Contact*  
- Blank/duplicate rows  
- Mixed formats: some columns as text, some as numbers  
- Need to compute/format *Profit Margin*

---

## 🧰 Step-by-Step Procedure

### 🔹 Step 1: Load Data into Power Query

1. Open Excel → Go to **Data** tab  
2. Select **Get Data → From Workbook**  
3. Choose the Excel file  
4. In **Navigator**, select the sheet and click **Transform Data**  
→ Power Query Editor opens.

---

### 🔹 Step 2: Column-by-Column Cleaning

#### 📅 Column 1: Date  
**Issue**: Contains unnecessary timestamps  
**Fix**:  
- Select column → `Transform > Data Type > Date`

---

#### 🧾 Column 2: Client  
**Issue**: Contains extra IDs in brackets  
**Example**: `AMAZON.COM, INC. (XNXS:AMZN)`  
**Goal**: Keep only `AMAZON.COM, INC.`  
**Fix**:  
- Split by delimiter `(`  
- Remove second part  
- Trim spaces  
- Format: `Capitalize Each Word`

---

#### 🧑‍💼 Column 3: Contact  
**Issue**: Inconsistent name formats and spacing  
**Fix**:  
- Split by space into 2–3 parts  
- Trim all parts  
- Merge back with space  
- Format: `Capitalize Each Word`

---

#### 🏢 Column 4: Department  
**Issue**: Combined department & location  
**Example**: `Cloud_Tech_Texas`  
**Fix**:  
- Split by `_`  
- Rename to: `Department`, `Country`  
- Format: `Capitalize Each Word`

---

#### 🌍 Column 5: Country  
**Created after splitting Department**

---

#### 💳 Column 6: Payment  
**Issue**: Blank entries  
**Fix**:  
- Select column → `Transform > Fill > Down`  
- Trim and capitalize entries (e.g., `Card`, `Paypal`, `Transfer`)

---

#### 💰 Column 7: Revenue  
**Issue**: Contains blanks  
**Fix**:  
- Set type: `Decimal Number`  
- Calculate **average**  
- Replace nulls with average  
- Round Up and format as `Currency`

---

#### 📈 Column 8: Profit  
✅ Already clean and consistent — no transformation needed.

---

#### 📊 Column 9: Profit Margin  
**Goal**: Compute new margin  
**Fix**:  
- Add Column → `Custom Column`:  
  ```excel
  ([Profit] / [Revenue]) * 100

