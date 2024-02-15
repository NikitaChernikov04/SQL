# 3
```sql
UPDATE products SET price = price * 0.875
WHERE products.category = 'Clothing'
UPDATE products SET price = price * 0.95
WHERE products.category != 'Clothing'
```

# 4
## Самая высокая цена
```sql
SELECT category, avg(price) 
FROM products
GROUP BY category
ORDER BY avg DESC   
LIMIT 1;
```
## Самая низкая цена 
```sql
SELECT category, avg(price) 
FROM products
GROUP BY category
ORDER BY avg ASC 
LIMIT 1;
```

# 5
```sql
DELETE FROM orders WHERE quantity
< (SELECT avg(quantity) FROM orders);
```
