# Ex.1
```
SELECT DISTINCT pizzeria.name, rating FROM pizzeria
CROSS JOIN menu
WHERE pizzeria.id NOT IN (SELECT pizzeria_id FROM person_visits)
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/dd564a16-f999-4b5f-a55f-7d2c6f0146f8)

# Ex.2
```
SELECT  missing_date::date FROM generate_series ('2022-01-01','2022-01-10', INTERVAL '1 DAY') AS missing_date 
FULL JOIN (
SELECT * FROM person_visits WHERE person_id = 1 OR person_id = 2 AND visit_date BETWEEN '2022-01-01' AND '2022-01-10')  as tab
ON missing_date = visit_date WHERE tab.person_id IS NULL
ORDER BY missing_date
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/83f09b32-a648-4408-bb1a-bc0f527e5fc8)

# Ex.3
```
SELECT
 COALESCE(p.name, '-'),
 tab.visit_date,
 COALESCE(pi.name, '-')
 FROM person p
 FULL JOIN (
 SELECT pizzeria_id, person_id, visit_date FROM person_visits
 WHERE visit_date BETWEEN '2022-01-01' AND '2022-01-03'
) tab ON tab.person_id = p.id
FULL JOIN pizzeria pi ON pi.id = tab.pizzeria_id
ORDER BY 1, 2, 3
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/d0e5f3c9-24fa-4af6-80e9-aa32f28eb1bc)

# Ex.4
```
WITH date_nika AS(
SELECT  missing_date::date FROM generate_series ('2022-01-01','2022-01-10', INTERVAL '1 DAY') AS missing_date )
SELECT date_nika.missing_date FROM date_nika
LEFT JOIN (
SELECT * FROM person_visits WHERE person_id = 1 OR person_id = 2 AND visit_date BETWEEN '2022-01-01' AND '2022-01-10') 
AS tab
ON date_nika.missing_date = tab.visit_date
WHERE tab.person_id IS NULL
ORDER BY date_nika.missing_date
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/1b18db3e-775b-4593-89b4-4b9dcbfb889b)

# Ex.5
```
SELECT m.pizza_name, pi.name, m.price FROM menu m
JOIN pizzeria pi ON m.pizzeria_id = pi.id
WHERE m.pizza_name IN ('mushroom pizza' , 'pepperoni pizza')
ORDER BY 1, 2
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/983424e8-22b2-49bd-a581-0c25c96d32dd)

# Ex.6
```
SELECT name
FROM person
WHERE gender = 'female' AND age > 25
ORDER BY name
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/61e54555-c669-40fd-9678-862cb57437cd)

# Ex.7
```
SELECT m.pizza_name, pi.name FROM person_order po
JOIN menu m ON po.menu_id = m.id
JOIN pizzeria pi ON pi.id = m.pizzeria_id
JOIN person p ON p.id = po.person_id
WHERE p.name IN ('Denis', 'Anna')
ORDER BY 1, 2
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/e171d308-0b0b-486e-ac22-cf216fc8acc8)

# Ex.8
```
SELECT p.name, pz.name FROM person_visits pv
JOIN person p ON pv.person_id = p.id
JOIN pizzeria pz ON pv.pizzeria_id = pz.id
WHERE pv.visit_date = '2022-01-08' AND p.name = 'Dmitriy'
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/fc5842fe-5c86-43fc-ae69-622ecb71311a)

# Ex.9
```
SELECT name FROM person p
JOIN person_order po ON p.id = po.person_id
JOIN menu m ON m.id = po.menu_id
WHERE (p.gender='male' AND p.address='Moscow' or p.address='Samara') AND (m.pizza_name = 'mushroom pizza' or m.pizza_name = 'pepperoni pizza')
ORDER BY p.name DESC
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/2a9eaa5b-1c9d-4ff6-8414-3d04d56698de)

# Ex.10
```
SELECT name FROM person p
JOIN person_order po ON p.id = po.person_id
JOIN menu m ON m.id = po.menu_id
WHERE (p.gender='female') AND (m.pizza_name = 'cheese pizza' or m.pizza_name = 'pepperoni pizza')
ORDER BY p.name DESC
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/f97ef22c-d5ff-4c2c-99d9-1d9b52fdc67e)

# Ex.11
```
SELECT per1.name AS person_name1, per2.name AS person_name2, per1.address AS common_address FROM person AS per1
JOIN person AS per2 ON per1.address = per2.address AND per1.name != per2.name
ORDER BY person_name1, person_name2, common_address
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/cfbe9e14-b879-4276-9062-0d035d647a39)
