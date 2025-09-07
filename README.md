# Layoffs — MySQL Cleaning & Exploratory Pipeline

**End-to-end MySQL scripts to clean and explore the `layoffs` dataset.**  
This repository contains a reproducible MySQL pipeline that cleans, standardizes, and explores the layoffs dataset to produce validated tables and summary analyses.

# Data Cleaning 

**Clean, standardize, and prepare the `layoffs` dataset using repeatable MySQL 8+ scripts.**  
This repo contains SQL scripts that (1) create safe staging copies, (2) remove exact and near-duplicates, (3) standardize textual fields and dates, (4) fill or remove null/blank values, and (5) tidy schema for downstream analysis.

## 🔎 Overview of transformations
Major transformations implemented in the scripts:

- **Staging & backups:** create staging tables (`layoffs_staging`, `layoffs_staging2`) to work on copies rather than the original table.  
- **Deduplication:** use `ROW_NUMBER()` over partition keys (company, location, industry, total_laid_off, percentage_laid_off, date, stage, country, funds_raised_millions) to find and remove duplicate rows.  
- **Standardization:** trim whitespace from `company`, normalize `industry` values (e.g., `Crypto%` → `Crypto`), and trim trailing punctuation in `country` values.  
- **Date conversion:** convert text `date` (format `%m/%d/%Y`) to actual `DATE` type and alter the column.  
- **Nulls & blanks:** convert empty strings to `NULL`, copy missing `industry` values by joining on company, and delete rows where both `total_laid_off` and `percentage_laid_off` are NULL.  
- **Schema cleanup:** remove temporary columns (e.g., `row_num`) after validation.

# Exploratory Analysis

After cleaning, the `layoffs_staging2` table is analyzed with a series of reproducible SQL queries to surface key metrics and trends. The exploratory scripts compute summary statistics, top companies/industries/countries by layoffs, temporal trends (monthly and yearly), company-year rankings, and rolling totals.

**Main analysis outputs**
- Global summary (max layoffs, date range, totals).  
- Top companies and industries by total layoffs.  
- Country-level aggregation of layoffs.  
- Yearly and monthly time series (including cumulative rolling totals).  
- Top companies per year (ranked lists).  
