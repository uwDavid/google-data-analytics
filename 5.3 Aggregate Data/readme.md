# Data Aggregation

## JOINS in SQL

| Join Type       | Result                                           |
| --------------- | ------------------------------------------------ |
| inner join      | obtain the interesction between A and B          |
| left join       | obtain all of A and interesction between A and B |
| right join      | obtain all of B and interesction between A and B |
| full outer join | obtain OR result between A and B                 |

General JOIN syntax:

```sql
SELECT
    table1.columns
    table2.columns
FROM
    table1
JOIN
    table2
ON table1.id_column = table2.id_column
```

## Alias

Used to rename tables columns.
Only lasts for the query.
Basic sytanx rules:

```sql
SELECT column_names AS col_alias
FROM table_name AS table_alias;
```

Examples

```sql
SELECT *
FROM warehouse_orders.Orders orders
JOIN
    warehouse_orders.Warehouse warehouse
ON
    orders.warehouse_id = warehouse.warehouse_id
```

## Count and Count Distinct

COUNT DISTINCT only counts unique values

```sql
SELECT *
    COUNT (DISTINCT warehouse.state) as num_states
FROM warehouse_orders.Orders orders
JOIN
    warehouse_orders.Warehouse warehouse
ON
    orders.warehouse_id = warehouse.warehouse_id
GROUP BY
    warehouse.state
```

## Subqueries

SQL queries nested inside another SQL query.
Inner query executes first => pass result to outer query for more processing.

```sql
SELECT
    station_id,
    num_bikes_available,
    (SELECT AVG(num_bikes_available)
    FROM ny_citibike_stations AS avg_num_bikes_available)
FROM ny_citibike_stations
```

WHERE Station example

```sql
SELECT station_id, name
FROM ny_citibike_stations
WHERE
    station_id IN
    (
        SELECT start_station_id
        FROM ny_citibike_trips
        WHERE
            usertype = 'Subscriber'
    )
```

## HAVING

HAVING allows us to add a filter to your query.
HAVING clause was added to SQL because WHERE keyword could not be used with aggregate functions.
For example, we can use WHERE and then GROUP BY.
But if we want to use GROUP BY and then WHERE, we will need to using HAVING.

```sql
SELECT
    Warehouse.warehouse_id,
    CONCAT(Warehouse.state, ' : ', Warehouse.warehouse_alias) AS warehouse_name,
    COUNT(Orders.order_id) AS number_of_orders,
    (
        SELECT
            COUNT(*)
        FROM warehouse_orders.Orders AS Orders
    ) AS total_orders,
    CASE
        WHEN COUNT(Orders.order_id)/(SELECT COUNT(*) FROM warehouse_orders.Orders Orders) <= 0.2
        THEN 'fulfilled 0-20% of Orders'

        WHEN COUNT(Orders.order_id)/(SELECT COUNT(*) FROM warehouse_orders.Orders Orders) > 0.2
        AND COUNT(Orders.order_id)/(SELECT COUNT(*) FROM warehouse_orders.Orders Orders) <= 0.6
        THEN 'fulfilled 21-60% of Orders'

        ELSE 'fulfilled more than 60% of Orders'
        END AS fulfillment_summary
FROM warehouse_orders.Warehouse Warehouse
LEFT JOIN wharehouse_orders.Orders Orders
ON Orders.warehouse_id = Warehouse.warehouse_id
GROUP BY
    Warehouse.warehouse_id,
    warehouse_name
HAVING
    COUNT(Orders.order_id) >0
```

## CASE

```sql
SELECT OrderID, Quantity,
CASE
    WHEN Quantity > 30 THEN 'The quantity is greater than 30'
    WHEN Quantity = 30 THEN 'The quantity is 30'
    ELSE 'The quantity is under 30'
END AS QuantityText
FROM OrderDetails;
```

## IF

```sql
SELECT OrderID, Quantity, IF(Quantity>10, "MORE", "LESS")
FROM OrderDetails;
```
