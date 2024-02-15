# 3
```sql
UPDATE products SET price = price * 0.875
WHERE products.category = 'Clothing'
UPDATE products SET price = price * 0.95
WHERE products.category != 'Clothing'
```

# 5
```sql
DELETE FROM orders WHERE quantity
< (SELECT avg(quantity) FROM orders);
```
