# Ex.2
```
SELECT (name,age) FROM person
WHERE address = 'Novosibirsk'
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/426874cf-97dd-4657-b46b-7a4bfef06ccc)

# Ex.3
```
SELECT name, age, gender
FROM person WHERE gender= 'female' AND address= 'Kazan'
ORDER BY name DESC
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/ed4d249b-c62e-4748-aed6-a6c67fb5bb9f)

# Ex.4
```
SELECT name,rating FROM pizzeria
WHERE rating BETWEEN 3.5 AND 5
ORDER BY rating DESC
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/ac25e35c-a279-4c85-9302-f5cfd8868114)

# Ex.5
```
SELECT DISTINCT person_id FROM person_visits
WHERE person_visits.visit_date BETWEEN '2022-01-01' AND '2022-01-04'
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/6fd99663-a957-460c-806e-b4311720b9b3)

# Ex.6
```
SELECT name FROM person
WHERE id IN(SELECT person_id FROM person_order 
		   WHERE menu_id= 2)
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/6b9929c8-189f-4119-9353-e2db821791b4)

# Ex.7
```
SELECT EXISTS(SELECT name FROM person WHERE name= 'Anna' )
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/8cf4eb28-0523-43f1-876b-3dcec6715b86)
