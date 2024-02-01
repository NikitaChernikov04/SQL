# Ex.1
```
SELECT pizza_name, price, name, visit_date FROM menu,
pizzeria, person_visits
WHERE person_id = '3' AND price BETWEEN 800 AND 1000
ORDER BY pizza_name, price DESC, name
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/c7a7ab3e-37cd-47a4-ad2d-823f1b61e95e)
# Ex.2
```
SELECT menu.id FROM menu
WHERE menu.id NOT IN (SELECT DISTINCT menu_id FROM person_order)
ORDER BY menu.id
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/12673db4-e71f-4876-94cc-1768152e2a6e)

# Ex.3
```
SELECT DISTINCT id FROM menu
EXCEPT
SELECT DISTINCT menu_id FROM person_order
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/e2c545d3-52a7-43ca-97a8-73fa1d70890f)

# Ex.4
```
WITH female AS (
	SELECT pi.name FROM pizzeria pi
	JOIN person_visits pv ON pv.pizzeria_id = pi.id
	JOIN person p ON pv.person_id = p.id
	WHERE p.gender='female'
), male AS (
	SELECT pi.name FROM pizzeria pi
	JOIN person_visits pv ON pv.pizzeria_id = pi.id
	JOIN person p ON pv.person_id = p.id
	WHERE p.gender='male'
)

(
	SELECT * FROM female
	EXCEPT ALL
	SELECT * FROM male
)
UNION
(
	SELECT * FROM male
	EXCEPT ALL
	SELECT * FROM female
)
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/8aa141e4-4f06-4e5c-afc4-17e25d4884e0)
