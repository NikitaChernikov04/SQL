## №175 Combine Two Tables

```sql
SELECT firstName, lastName, city, state FROM Person 
LEFT JOIN Address ON Person.personID = Address.personID
```

