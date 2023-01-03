## Department Highest Salary

<details>
<summary>Schema</summary>

```sql
Create table If Not Exists Employee (id int, name varchar(255), salary int, departmentId int)
Create table If Not Exists Department (id int, name varchar(255))
Truncate table Employee
insert into Employee (id, name, salary, departmentId) values ('1', 'Joe', '70000', '1')
insert into Employee (id, name, salary, departmentId) values ('2', 'Jim', '90000', '1')
insert into Employee (id, name, salary, departmentId) values ('3', 'Henry', '80000', '2')
insert into Employee (id, name, salary, departmentId) values ('4', 'Sam', '60000', '2')
insert into Employee (id, name, salary, departmentId) values ('5', 'Max', '90000', '1')
Truncate table Department
insert into Department (id, name) values ('1', 'IT')
insert into Department (id, name) values ('2', 'Sales')
```
</details>
<br />

Table: `Employee`

```
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| id           | int     |
| name         | varchar |
| salary       | int     |
| departmentId | int     |
+--------------+---------+
id is the primary key column for this table.
departmentId is a foreign key of the ID from the Department table.
Each row of this table indicates the ID, name, and salary of an employee. It also contains the ID of their department.
```

Table: `Department`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| name        | varchar |
+-------------+---------+
id is the primary key column for this table.
Each row of this table indicates the ID of a department and its name.
```

Write an SQL query to find employees who have the highest salary in each of the departments.

Return the result table in any order.

<details>
<summary>Example 1</summary>

```
Input: 
Employee table:
+----+-------+--------+--------------+
| id | name  | salary | departmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Jim   | 90000  | 1            |
| 3  | Henry | 80000  | 2            |
| 4  | Sam   | 60000  | 2            |
| 5  | Max   | 90000  | 1            |
+----+-------+--------+--------------+
Department table:
+----+-------+
| id | name  |
+----+-------+
| 1  | IT    |
| 2  | Sales |
+----+-------+
Output: 
+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Jim      | 90000  |
| Sales      | Henry    | 80000  |
| IT         | Max      | 90000  |
+------------+----------+--------+
Explanation: Max and Jim both have the highest salary in the IT department and Henry has the highest salary in the Sales department.
```
</details>


<details>
<summary>Solution 1</summary>

```sql
SELECT 
    Department.name as Department,
    Employee.name as Employee,
    Employee.salary as Salary
FROM Employee 
JOIN 
    (
        SELECT departmentId, MAX(salary) as max_salary 
        FROM Employee 
        GROUP BY departmentId
    ) Salary 
ON Salary.departmentId = Employee.departmentId
JOIN Department ON Department.id = Employee.departmentId 
WHERE Employee.salary = Salary.max_salary
```
</details>

<details>
<summary>Solution 2</summary>

```sql
SELECT Department, Employee, Salary FROM (
    SELECT *, rank() OVER(PARTITION BY Department ORDER BY Salary DESC) as Highest_Salary 
    FROM (
        SELECT 
            d.name AS Department,
            e.name AS Employee,
            e.salary AS Salary
        FROM Department d 
        INNER JOIN Employee e 
        ON d.id = e.departmentId
    ) X
) Y
WHERE Highest_Salary < 2
```
</details>