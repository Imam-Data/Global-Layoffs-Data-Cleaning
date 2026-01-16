# Global Layoffs Data Cleaning Project

## Project Overview
**Objective**: Transform a raw, messy dataset of global layoffs (2020-2025) into a high-quality, analysis-ready format for SQL database integration.

**Tools Used**: Microsoft Excel (Remove Duplicates, Pivot Tables, Text to Columns, Custom Formatting, Data Validation)

**Time to Complete**: ~3 hours

**Dataset**: 4,249 raw records → 1,911 clean, validated records

---

## Business Impact

### Why This Matters
- **Time Efficiency**: Clean data eliminates the need for repetitive null-handling in every SQL query
- **Data Accuracy**: Removed 2,338 unusable records (55% noise reduction) ensuring only actionable data remains
- **Database Compatibility**: Standardized ISO 8601 date format enables seamless MySQL import and chronological analysis
- **Quality Assurance**: Systematic cleaning process ensures 100% data integrity for downstream analysis

---

## The Problem (Raw Data Challenges)

The initial dataset (`layoffs_raw.csv`) contained **4,249 rows** with critical quality issues:

| Issue | Impact |
|-------|--------|
| **Format Incompatibility** | Dates stored as text (MM/DD/YYYY), unusable for SQL sorting/filtering |
| **High Null Rate** | 55% of records contained blanks in key metrics (`total_laid_off` AND `percentage_laid_off`) |
| **Potential Duplicates** | Risk of inflated counts without validation |
| **Inconsistent Text** | Possible typos in categorical fields (Industry, Country, etc.) |

---

## Cleaning Process (Step-by-Step)

### Step 1: Data Integrity Check (Duplicate Detection)
**Objective**: Ensure every record is unique before processing.

**Action**: 
- Applied Excel's `Remove Duplicates` tool across all columns
- Scanned entire dataset for exact row matches

**Result**: ✅ **No duplicates found** - Dataset integrity confirmed

![Duplicate Check](1_duplicate_proof.png)
*System confirmation: Raw dataset contained 0 duplicate records*

---

### Step 2: Standardization Audit (Quality Control)
**Objective**: Detect spelling inconsistencies and typos in categorical columns.

**Action**: 
- Created Pivot Table on `Industry` column to group unique values
- Manually inspected all categories for variations (e.g., "Crypto" vs "CryptoCurrency")

**Result**: ✅ **Verified Clean** - All industry names standardized, no inconsistencies detected

![Industry Audit](2_industry_audit.jpg)
*Pivot table summary used for categorical validation*

---

### Step 3: Date Formatting (Text → SQL-Compatible Format)
**Objective**: Convert `Date` column from text to proper Date object compatible with MySQL.

**Problem**: 
- Raw dates stored as text with inconsistent format (MM/DD/YYYY)
- Unusable for chronological sorting or date-based queries

**Action**: 
1. Used `Text to Columns` wizard to parse date components
2. Applied custom formatting: `YYYY-MM-DD` (ISO 8601 standard)
3. Verified data type changed from Text to Date

**Result**: 

**❌ BEFORE (Raw Text):**

![Date Before](3a_date_before.png)

**✅ AFTER (SQL Standard):**

![Date After](3b_date_after.jpg)

---

### Step 4: Removing Null Values (Data Quality Filter)
**Objective**: Eliminate rows that provide zero analytical value.

**Problem**: 
- Rows where **BOTH** `total_laid_off` AND `percentage_laid_off` were NULL (blank)
- These records contain no layoff information whatsoever

**Key Decision**: 
- **Why delete instead of impute?** If both metrics are missing, there's no baseline data to work with. Imputation would create false information.

**Action**: 
1. Applied filter: Show rows where both columns = `(Blanks)`
2. Deleted **2,338 unusable rows**
3. Verified remaining data has at least one valid metric

**Result**: 

**❌ BEFORE (4,249 Rows):**

![Nulls Before](4a_null_before.jpg)
*Filter shows '(Blanks)' present. Original count: 4,249 rows*

**✅ AFTER (1,911 Rows):**

![Nulls After](4b_null_after.png)
*Blanks removed. Final count: 1,911 rows ready for SQL*

---

## Final Summary

### Quality Metrics
| Metric | Value | Status |
|--------|-------|--------|
| **Completeness** | 100% | ✅ No critical nulls in final dataset |
| **Uniqueness** | 100% | ✅ No duplicate records |
| **Validity** | 100% | ✅ Date format verified (YYYY-MM-DD) |
| **Consistency** | 100% | ✅ Categorical fields standardized |

### Transformation Overview
| Stage | Row Count | Action Taken |
|-------|-----------|--------------|
| Original Dataset | 4,249 | Raw data with quality issues |
| After Null Removal | 1,911 | Removed 2,338 unusable records (55% noise) |
| **Final Clean Dataset** | **1,911** | **SQL-ready, high-quality data** |

---

## 📁 Repository Files

- `layoffs_raw.csv`: Original messy dataset
- `layoffs_cleaned_final.csv`: Processed dataset (CSV UTF-8 format)
- `README.md`: Project documentation
- Screenshots: Process evidence (before/after comparisons)

---

## 🔗 What's Next?

This cleaned dataset powers downstream analysis projects:

- **[Economic Trend Analysis](https://github.com/Imam-Data/World-Layoffs-Data-Analysis)** - SQL deep-dive using MySQL CTEs and Window Functions

---

## Key Learnings

1. **Data cleaning is 70% of analysis work** - Investing time upfront saves hours of troubleshooting later
2. **Visual validation matters** - Screenshots prove quality and build stakeholder trust
3. **Document your decisions** - Explaining "why delete vs impute" shows analytical thinking
4. **Standardization is critical** - ISO date formats prevent integration headaches

---

## Technical Skills Demonstrated

- Data Quality Assessment
- Excel Power Tools (Remove Duplicates, Text to Columns, Pivot Tables)
- Data Validation & Auditing
- ISO 8601 Date Standardization
- Null Handling Strategies
- Documentation & Process Visualization

---

## 📧 Contact

**GitHub**: [@Imam-Data](https://github.com/Imam-Data)

---
