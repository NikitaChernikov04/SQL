# Ex.00
```sql
CREATE TABLE person_discounts (
	id BIGINT PRIMARY KEY, 
	person_id BIGINT NOT NULL , 
	pizzeria_id BIGINT NOT NULL , 
	dsicount FLOAT DEFAULT NULL , 
	CONSTRAINT fk_person_discount_person_id FOREIGN KEY (person_id) REFERENCES person(id), 
	CONSTRAINT fk_person_discount_pizzeria_id FOREIGN KEY (pizzeria_id) REFERENCES pizzeria(id) 
	); 
	SELECT * FROM person_discounts;
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/37626f08-3b0a-4c4b-96e8-5d2411765df3)

# Ex.01
```sql
WITH amount_of_orders as (
	SELECT po.person_id, m.pizzeria_id, COUNT(*) FROM person_order po
	JOIN menu m ON m.id = po.menu_id
	GROUP BY 1, 2
	ORDER BY 1, 2
)

INSERT INTO person_discounts (
	SELECT 
		ROW_NUMBER() OVER(ORDER BY 1) as id,
		person_id,
		pizzeria_id,
		CASE
			WHEN count = 1 THEN 10.5
			WHEN count = 2 THEN 22
			ELSE 30
		END
	FROM amount_of_orders
);
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/5b9a04fd-6831-4c2e-b36d-caa96ef2ab15)

# Ex.02
```sql
SELECT p.name, m.pizza_name, m.price, (m.price-(m.price/100) * pd.discount) as discount,
	pz.name
FROM person p
JOIN person_order po ON po.person_id = p.id
JOIN menu m ON m.id = po.menu_id
JOIN pizzeria pz ON pz.id = m.pizzeria_id
JOIN person_discounts pd ON pd.person_id = po.person_id AND pd.pizzeria_id = m.pizzeria_id 
ORDER BY 1;
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/ecdcfe8d-cc32-4926-a86e-b7c22920ac51)
