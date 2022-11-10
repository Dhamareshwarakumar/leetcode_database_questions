## Second Highest Salary

<details>
<summary>Schema</summary>

```sql
Create table If Not Exists Employee (id int, salary int);

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

Write an SQL query to report the second highest salary from the Employee table. If there is no second highest salary, the query should report null.

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

Output: 
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
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

Output: 
+---------------------+
| SecondHighestSalary |
+---------------------+
| null                |
+---------------------+
```
</details>
<br />

<details>
<summary>Solution 1</summary>

```sql
SELECT (SELECT DISTINCT salary from Employee ORDER BY salary DESC LIMIT 1 OFFSET 1) AS SecondHighestSalary;
```
</details>

<details>
<summary>Solution 2</summary>

```sql
SELECT  MAX(SALARY) AS SecondHighestSalary FROM EMPLOYEE WHERE SALARY <>(SELECT MAX(SALARY) FROM EMPLOYEE);
```
</details>