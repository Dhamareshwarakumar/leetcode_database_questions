## Nth Highest Salary

<details>
<summary>Schema</summary>

```SQL
Create table If Not Exists Employee (Id int, Salary int);

Truncate table Employee;

insert into Employee (id, salary) values ('1', '100');
insert into Employee (id, salary) values ('2', '200');
insert into Employee (id, salary) values ('3', '300');
```
</details>
<br />

Table: `Employee`
```
+-------------+------+
| Column Name | Type |
+-------------+------+
| id          | int  |
| salary      | int  |
+-------------+------+
id is the primary key column for this table.
Each row of this table contains information about the salary of an employee.
```

Write an SQL query to report the nth highest salary from the Employee table. If there is no nth highest salary, the query should report null.

The query result format is in the following example.

 
<details>
<summary>Example 1</summary>

```
Input: 

Employee table:
+----+--------+
| id | salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+

n = 2

Output: 
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```
</details>

<details>
<summary>Example 2</summary>

```
Input: 

Employee table:
+----+--------+
| id | salary |
+----+--------+
| 1  | 100    |
+----+--------+

n = 2

Output: 
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| null                   |
+------------------------+
```
</details>

<details>
<summary>Solution</solution>

```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
    DECLARE M INT;
    SET M = N - 1;
  RETURN (
      SELECT DISTINCT salary from Employee ORDER BY salary DESC LIMIT 1 OFFSET M
  );
END
```
</details>