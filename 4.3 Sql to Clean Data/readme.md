# SQL Functions

`CAST()` - Converts one data type to another 
```sql
SELECT CAST(purchase_price AS FLOAT64)
FROM customer_data.customer_purchase
ORDER BY CAST(purchase_price AS FLOAT64) DESC
```
```sql
SELECT 
    CAST(date AS date) AS date_only,
    purchase_price
FROM customer_data.customer_purchase
WHERE 
    date BETWEEN '2020-12-01' AND '2020-12-31'
```

`CONCAT()` - Concatenates two strings 
```sql
SELECT 
    CONCAT(product_code, product_color) AS new_product_code
FROM 
    customer_data.customer_purchase
WHERE 
    product = 'couch'
```

`COALESCE()` - used to return non-null values in a list
If product names aren't available, then give us the product_code
```sql
SELECT 
    COALESCE(product, product_code) AS product_info
FROM customer_data.customer_purchase
```
