# Data Analysis Basics

## Analysis Process
1. Organize data - collecting data for your requirements
2. Format and adjust data - rearranging data to make it easier to work with
3. Get input from others - solicit info from others to help you make decisions 
4. Transform data - involves identifying relationships and patterns

## Sorting in SQL
This is done by using `ORDER BY`
```sql
SELECT 
  *
FROM 
  `bigquery-public-data.sdoh_cdc_wonder_natality.county_natality` 
ORDER BY
  Births
ASC
LIMIT 
  10
```

