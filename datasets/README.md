# Datasets Directory - Zion Tech Hub Reform Analysis Hackathon

This directory contains the data files used in the analysis for the **Zion Tech Hub Reform Analysis Hackathon Project**, which focuses on historical import data of electrical machinery under HS Code 85 and their associated tariffs.

---

## Data Sources

### 1. **ZTH Data Analysis Hackathon.xlsx**
- **Source**: Provided by Zion Tech Hub.
- **Description**: Contains detailed records on imports of electrical machinery.
- **Columns Included**:
  - Custom Office
  - Reg Number
  - Reg. Date
  - Importer
  - Item Nbr
  - HS Code
  - HS Description
  - FOB Value (N)
  - CIF Value (N)
  - Total Tax (N)
  - Receipt Number
  - Receipt Date
  - Mass (KG)
  - Country Of Origin
  - Country Of Supply
  - Nbr Of Container
  - Container Nbr
  - Container Size
- **Format**: `.xlsx`
- **Original Size**: 133,736 rows × 18 columns

### 2. **cet_tariff.xlsx**
- **Source**: Nigeria Trade Portal + supplementary HS codes from the Nigeria Customs Service tariff document.
- **Description**: Contains expected tariff components for HS Code 85 items.
- **Columns Included**:
  - CET Code
  - Description
  - SU
  - ID
  - VAT
  - LVY
  - EXC
  - DOV
- **Format**: `.xlsx`
- **Final Size After Filtering & Cleaning**: 350 rows × 2 columns (`HS_Code`, `Exp_Tax_Rate`)

---

## Data Cleaning and Transformation

1. **ZTH Dataset**:
   - Removed empty and duplicate columns.
   - Dropped columns with excessive missing values.
   - Standardized column names and corrected data types.
   - Reduced from 133,736 rows × 18 columns to 110,369 rows × 14 columns.
   - Saved as: `clean_data.xlsx`

2. **CET Tariff Dataset**:
   - Filtered to include only HS Code 85 items.
   - Computed expected tax rate by summing relevant tax columns.
   - Manually added missing HS codes using official customs tariff documents.
   - Reduced and saved with relevant columns: `cet_tariff.xlsx`

---

## Files Included

- **ZTH Data Analysis Hackathon.xlsx** – Raw dataset (original format).
- **clean_data.xlsx** – Cleaned and transformed version of the ZTH dataset.
- **cet_tariff.xlsx** – Tariff information relevant to HS Code 85 goods.
- **merged_data.csv** – Contains the cleaned and enriched(cet_tariff) historical import data.
- **forecasted_imports.csv** – Holds time-series forecast (prophet) results of import volumes.
- **forecasted_tax_revenue.csv** – Holds time-series forecast (prophet) results of tax revenue.
- **fund_df.csv** – Shows strategic allocation of a ₦100B innovation fund across high-impact categories.
- **hs_growth_df.csv** – Summarizes growth trends for top HS codes with high import volume and substitution potential.

Note: All CSV files were generated and exported from the analysis notebook and subsequently loaded into Power BI for modeling and visualization.
---

