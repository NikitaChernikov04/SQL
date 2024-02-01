# Ex.1
```
SELECT pizzeria_id, pizza_name FROM menu 
UNION 
SELECT id, name FROM person
ORDER BY pizzeria_id, pizza_name
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/40f1061b-100a-4231-b72d-a328899a8cc8)

# Ex.2
```
SELECT DISTINCT person.name, menu.pizza_name FROM person
JOIN menu ON person.id = menu.pizzeria_id
ORDER BY person.name, menu.pizza_name
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/9ea8b600-cd46-43b4-8d10-7a513da0179a)

# Ex.3
```
SELECT po.order_date, po.person_id FROM person_order po
JOIN person_visits pv ON po.person_id = pv.person_id AND po.order_date = pv.visit_date
ORDER BY po.order_date ASC, po.person_id DESC
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/e4e660fd-bdaf-4b60-a48f-831125a81585)

# Ex.4
```
SELECT person_id FROM person_order
WHERE order_date = '2022-01-07'
EXCEPT
SELECT person_id FROM person_visits
WHERE visit_date = '2022-01-07'
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/7bb13db9-ee0d-41b7-8844-f363d304869a)

# Ex.5
```
SELECT * FROM person, pizzeria
ORDER BY person.id, pizzeria.id
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/8fce41c7-daad-44fa-b6b3-907eaa80ae53)

# Ex.6
```
SELECT action_date, p.name FROM
(
 SELECT order_date AS action_date, person_id FROM person_order
 INTERSECT ALL
 SELECT visit_date,person_id FROM person_visits
) as tab
JOIN person p ON tab.person_id = p.id
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/efc938ee-7a86-48f2-b99a-c57821ed7e6a)

# Ex.7
```
SELECT po.order_date, CONCAT(p.name, ' (age:', p.age, ')') AS personal_info FROM person_order po
JOIN person p ON po.person_id = po.person_id
ORDER BY po.order_date, p.name, p.age
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/9494314e-a541-4173-95a2-2c722d0e3c16)

# Ex.8
```
SELECT po.order_date, CONCAT(p.name, ' (age:', p.age, ')') AS personal_info FROM person_order po
NATURAL JOIN person p
ORDER BY po.order_date, p.name, p.age
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/857713f1-bd8d-4666-b20a-569c33afadbd)

# Ex.9
```
SELECT name
FROM pizzeria
WHERE id NOT IN (
    SELECT DISTINCT pizzeria_id
    FROM person_visits
)
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/cff1c5f7-4eb5-4262-9283-f7819d390e33)


# Ex.10
```
SELECT person.name AS person_name, menu.pizza_name AS pizza_name, pizzeria.name AS pizzeria_name FROM person_order
JOIN person ON person_order.person_id = person.id
JOIN menu ON person_order.id = menu.id
JOIN pizzeria ON person_order.id = pizzeria.id
ORDER BY person_name ASC, pizza_name ASC, pizzeria_name ASC
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/fec17612-d67a-44f3-95dc-9d6e96d6e073)
