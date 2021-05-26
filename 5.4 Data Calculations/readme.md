# Data Calculations

## SUMIF

The basic syntax of a SUMIF function is: =SUMIF(range, criterion, sum_range)
The basic syntax for SUMIFS: =SUMIFS(sum_range, criteria_range1, criterion1, [criteria_range2, criterion2, ...])

Count if is similar

## SUMPRODUCT

`=sumproudct(array1, [array2,...])`
Will return the multiplication of all rows of a column then add them together

## SQL Calculations

```sql
SELECT
    columnA,
    columnB,
    columnA+columnB AS columnX
FROM
    tablename
```

## EXTRACT

Extract command allow us to pull one part of a given date to use

```sql
SELECT
    EXTRACT(YEAR from STARTTIME) AS year,
    COUNT(*) AS number_of_rides
FROM
    ny_citibike_trips
GROUP BY year
ORDER BY year
```

## Data Validation

Check for:

1. Data type
2. Data range
3. Data contraints
4. Data consistency
5. Data structure
6. Code validation

## Temporay Table

Temporary tables are automatically deleted after ending the session in a SQL database.
To set up a temporary table use `WITH`

```sql
WITH new_table_data AS (
    SELECT *
    FROM Existing_table
    WHERE tripduration >=60
)
```

```sql
WITH longest_used_bike AS (
    SELECT
        bikeid,
        SUM(duration_minutes) AS trip_duration
    FROM
        austin_bikeshare.bikeshare_trips
)

SELECT
    trips.start_station_id,
    COUNT(*) AS trip_ct
FROM
    longest_used_bike AS longest
INNER JOIN
    autin_bikeshare.bikeshare_trips AS trips
ON longest.bikeid = trips.bikeid
```

## SELECT INTO

Another way to create temp table is to use `SELECT INTO` or `CREATE TABLE` clauses
The `SELECT INTO` clause copies data from one table into a new table, but doesn’t add the new table to the database.
It’s useful if you want to make a copy of a table with a specific condition, with a WHERE clause.

Google Big Query doesn't recognize SELECT INTO,

```sql
SELECT *
INTO AfricaSales
FROM GlobalSales
WHERE Region = "Africa"
```

## CREATE TABLE

If the code is hard to replicate, making a temp table this way will allow you to access it later.

```sql
CREATE table_name (
    column1 datatype,
    column2 datatype
)

DROP TABLE table_name
```
