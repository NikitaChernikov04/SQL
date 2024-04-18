## №175 Combine Two Tables

```sql
SELECT firstName, lastName, city, state FROM Person 
LEFT JOIN Address ON Person.personID = Address.personID
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/5c5bada0-cfca-4b24-81d4-500673af9681)

## №176 Second Highest Salary

```sql
SELECT MAX(Salary) as SecondHighestSalary FROM Employee
WHERE Salary < (SELECT MAX(Salary) FROM Employee)
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/91fb026a-f1fd-476e-ba3d-4a6c6e4a3b2a) ![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/9981e918-742a-4feb-bc06-c1123fc089f5)

## №177 

```sql
CREATE OR REPLACE FUNCTION NthHighestSalary(N INT) RETURNS TABLE (Salary INT) AS $$
BEGIN
  RETURN QUERY (
    -- Write your PostgreSQL query statement below.
    SELECT DISTINCT tab.salary FROM (
    SELECT Employee.salary, DENSE_RANK() OVER(ORDER BY Employee.salary DESC) as rank FROM Employee
    ) as tab
    WHERE rank = N     
  );
END;
$$ LANGUAGE plpgsql;
```
![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/144c67ba-c6f2-48c5-9d65-e08834dce4af) ![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/fbb7190c-8972-4c38-98da-c62d01e1da5c)

## №178 Rank Scores

```sql
SELECT score, DENSE_RANK() OVER(ORDER BY score DESC) as rank FROM Scores
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/9f8c0c27-8e1d-4ae4-b731-dc26480791cc)


## №181 Employees Earning More Than Their Managers

```sql
SELECT name AS "Employee" FROM Employee e
WHERE (e.managerId IS NOT NULL) 
AND (e.salary > (SELECT salary FROM Employee WHERE Employee.id = e.managerId))
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/89df8e72-5df8-4cc3-868f-0fd574f09b9e)


##  №182 Duplicate Emails

```sql
SELECT email FROM person
GROUP BY email
HAVING COUNT(email) > 1;
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/87045f42-78be-4e08-a6ca-52294127d07a)


## №183 Customers Who Never Order

```sql
SELECT cust.name AS "Customers" FROM Customers cust
LEFT JOIN Orders ord ON cust.id = ord.customerID
WHERE ord.customerID IS NULL;
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/aacceeda-630c-4cad-9e30-849e14c28a23)


## №184 Department Highest Salary

```sql
SELECT d.name AS Department, e.name AS Employee, e.salary AS Salary
FROM (
    SELECT departmentId, MAX(salary) AS max_salary
    FROM Employee
    GROUP BY departmentId
) AS max_salaries
JOIN Employee e ON e.departmentId = max_salaries.departmentId AND e.salary = max_salaries.max_salary
JOIN Department d ON e.departmentId = d.id;
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/1ce6184a-26a3-4bac-928e-6fdcbb2a91ee)


## №511 Game Play Analysis I

```sql
SELECT player_id, MIN(event_date) AS first_login FROM Activity
GROUP BY player_id
ORDER BY player_id;
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/defd7a0e-b756-443c-8294-75958f325b60)


## №570 Managers with at Least 5 Direct Reports

```sql
SELECT e1.name
FROM Employee AS e1
INNER JOIN Employee AS e2
ON e1.id = e2.managerId
GROUP BY e2.managerId, e1.name
HAVING COUNT(e2.managerId) >= 5
```

![image](https://github.com/NikitaChernikov04/SQL/assets/113566014/9029b311-89a5-4b19-9d79-8a9f3277f8fb)
