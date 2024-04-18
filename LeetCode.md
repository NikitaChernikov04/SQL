## №175 Combine Two Tables

```sql
SELECT firstName, lastName, city, state FROM Person 
LEFT JOIN Address ON Person.personID = Address.personID
```


## №176 Second Highest Salary

```sql
SELECT MAX(Salary) as SecondHighestSalary FROM Employee
WHERE Salary < (SELECT MAX(Salary) FROM Employee)
```


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


## №178 Rank Scores

```sql
SELECT score, DENSE_RANK() OVER(ORDER BY score DESC) as rank FROM Scores
```


## №181 Employees Earning More Than Their Managers

```sql
SELECT name AS "Employee" FROM Employee e
WHERE (e.managerId IS NOT NULL) 
AND (e.salary > (SELECT salary FROM Employee WHERE Employee.id = e.managerId))
```


##  №182 Duplicate Emails

```sql
SELECT email FROM person
GROUP BY email
HAVING COUNT(email) > 1;
```


## №183 Customers Who Never Order

```sql
SELECT cust.name AS "Customers" FROM Customers cust
LEFT JOIN Orders ord ON cust.id = ord.customerID
WHERE ord.customerID IS NULL;
```


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


## №511 Game Play Analysis I

```sql
SELECT player_id, MIN(event_date) AS first_login FROM Activity
GROUP BY player_id
ORDER BY player_id;
```


## №570 Managers with at Least 5 Direct Reports

```sql
SELECT e1.name FROM Employee AS e1
JOIN Employee AS e2 ON e1.id = e2.managerId
GROUP BY e2.managerId, e1.name
HAVING COUNT(e2.managerId) >= 5
```


## №1193 Monthly Transactions I

```sql
SELECT 
    to_char(trans_date, 'YYYY-MM') as month,
    country,
    COUNT(trans_date) as trans_count,
    SUM(CASE WHEN state = 'approved' then 1 else 0 end) as approved_count,
    SUM(amount) as trans_total_amount,
    SUM(CASE WHEN state = 'approved' then amount else 0 end) as approved_total_amount
FROM transactions 
GROUP BY 1, 2;
```


