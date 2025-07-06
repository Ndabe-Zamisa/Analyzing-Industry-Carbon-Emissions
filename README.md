# 🌍 Carbon Emissions Analysis with SQL

This project analyzes industry-level carbon emissions using SQL on real-world data. The analysis was conducted in [DataCamp’s DataLab](https://www.datacamp.com/datalab/w/900f3193-daff-4559-b8ea-40035869947e/print-notebook/notebook.ipynb), focusing on **Product Carbon Footprints (PCFs)** — greenhouse gas emissions attributed to products across various industries.

## 📊 Project Overview

- **Goal**: Identify industries contributing most to global carbon emissions.
- **Data Source**: Nature.com & The Carbon Catalogue
- **Database**: PostgreSQL
- **Table Analyzed**: `product_emissions`
- **Skills Used**: SQL querying, data aggregation, filtering, grouping, ordering

## 📁 Dataset Structure

The dataset includes the following columns:

| Field                         | Data Type   | Description                                                 |
|------------------------------|-------------|-------------------------------------------------------------|
| `id`                         | VARCHAR     | Unique record ID                                            |
| `year`                       | INT         | Year of recorded emissions                                  |
| `product_name`               | VARCHAR     | Name of the product                                         |
| `company`                    | VARCHAR     | Name of the company                                         |
| `country`                    | VARCHAR     | Country of the company                                      |
| `industry_group`             | VARCHAR     | Industry classification                                     |
| `weight_kg`                  | NUMERIC     | Weight of the product in kilograms                          |
| `carbon_footprint_pcf`       | NUMERIC     | Total product carbon footprint (CO2 equivalent)             |
| `upstream_percent_total_pcf`| VARCHAR     | Emissions during raw material and supply chain stages       |
| `operations_percent_total_pcf`| VARCHAR    | Emissions during product manufacturing                      |
| `downstream_percent_total_pcf`| VARCHAR    | Emissions during distribution, usage, and disposal          |

## 🔍 Key Analysis

The analysis focused on:
- Total carbon footprint by industry
- Number of companies reporting emissions in each industry
- Filtering to use only the most recent year of data

### Sample Query:
```sql
SELECT industry_group, COUNT(DISTINCT company) AS num_companies,
       ROUND(SUM(carbon_footprint_pcf), 1) AS total_industry_footprint
FROM product_emissions
WHERE year IN (SELECT MAX(year) FROM product_emissions)
GROUP BY industry_group
ORDER BY total_industry_footprint DESC;
