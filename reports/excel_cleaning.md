# 🧼 Data Cleaning Process

This document outlines the detailed data cleaning steps carried out using **Microsoft Excel 2024** to prepare the import dataset for analysis in the _Zion Tech Hub Reform Analytics Hackathon_.

---
## 📑 ZTH Data Analytics Hackathon.xlsx cleaning
## 📥 Raw Data Import

- File format: `.xlsx`
- Initial shape: **133,737 rows**, **18 columns**
- Converted data to a **Table** via `Insert → Table` for easier filtering and management.

---

## 🧠 Data Understanding & Initial Checks

- **Deleted** first column (empty).
- **Checked for duplicates**: None found.
- **Blank % calculation per column** using Excel formula:  
  `=(COUNTBLANK(Table1[column])/133736) * 100`
  
  Results:
  - `Container_Size`: 50.76%
  - `Container_Number`: 50.74%
  - `Receipt_Date`: 2.64%
  - `Receipt_Number`: 2.64%

---

## 🛠️ Column Cleaning & Transformation

- **Standardized column names**: Replaced spaces with underscores (e.g., `Importer` → `Importer_Code`, etc.).
- **Split** `Importer` column:
  - `Importer_Code`: `=TEXTBEFORE([@Importer], " -")`
  - `Importer_Name`: `=TRIM(TEXTAFTER([@Importer], "- "))`
  - Deleted original `Importer` column.
- **HS Code formatting**: Converted to number format.

---

## 🔢 Numerical Data Formatting

Applied to:
- `FOB_Value(N)`
- `CIF_Value(N)`
- `Total_Tax(N)`
- `Mass(KG)`
- `Nbr_of_Containers`

Steps:
- Converted text to number using `Value()` or ribbon → Format Cells → Number.

---

## 🧽 Categorical Cleanup

- Applied `Find & Replace` and `TRIM()` to clean:
  - Removed special characters: `#`, `"`, `___`, etc.
  - Standardized country names:
    - `Viet Nam` → `Vietnam`
    - `Korea Republic of` → `South Korea`
    - `Korea Democratic People's Rep. of` → `North Korea`
    - `Holy See (Vatican)` → `Vatican`

---

## ❗ Anomaly Detection

- Identified and removed rows where `FOB_Value(N)` > `CIF_Value(N)`:
  - Formula used: `=IF([@[FOB_Value(N)]] > [@[CIF_Value(N)]], "yes", "no")`
  - **564 rows** removed.

---

## 🗃️ Column Pruning

Removed the following columns:
- `Container_Number`
- `Container_Size`
- `Receipt_Date`
- `Receipt_Number`

Rationale: Primarily administrative with limited analytical value, plus high missingness.

---

## 📉 Final Row & Column Count

- **Duplicates removed**: `22,798`
- **Final shape**: `110,369 rows`, `14 columns`

---

## 💾 Export

Saved the cleaned dataset as:
- **`clean_data.xlsx`**

---

## 📑 CET Tariff Matching & Cleaning

### Data Integration

- Copied **CET_Tariff.xlsx** into a new sheet (`CET`) in the same workbook.
- Matched HS codes from `cleaned_data.xlsx` using:  
  `=IF(ISNUMBER(MATCH([@[HS_Code]], Sheet1!A:A, 0)), "Yes", "No")`
- Added missing HS codes manually using functional descriptions aligned with the **[Custom tariff document](https://customs.gov.ng/wp-content/uploads/2022/08/CET-rules.pdf)**.

### CET Sheet Cleanup

- Removed non-relevant columns: `Description`, `DOV`, `SU`, `EXC`
- Renamed columns to match cleaned dataset
- Calculated `Expected_Tax_Rate`:
  - Formula: `ID + LVY + VAT`
- Retained only: `HS_Code`, `Expected_Tax_Rate`
- Final CET shape: **259 rows**, **2 columns**

---

## 💾 Export

Saved as:
- **`cet_tariff.xlsx`**

---

> _This meticulous cleaning process ensures a reliable foundation for fiscal analysis, forecasting, and strategic modeling._
