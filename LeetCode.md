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









