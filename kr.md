# 3
```sql
UPDATE products SET price = price * 0.875
WHERE products.category = 'Clothing'
UPDATE products SET price = price * 0.95
WHERE products.category != 'Clothing'
```

# 4
```sql
Найти категорию товаров с самой высокой средней ценой, и категорию с самой низкой средней ценой. 

# 5
```sql
DELETE FROM orders WHERE quantity
< (SELECT avg(quantity) FROM orders);
```
