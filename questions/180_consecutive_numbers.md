## Consecutive Numbers

<details>
<summary>Schema</summary>

```sql
Create table If Not Exists Logs (id int, num int)
Truncate table Logs
insert into Logs (id, num) values ('1', '1')
insert into Logs (id, num) values ('2', '1')
insert into Logs (id, num) values ('3', '1')
insert into Logs (id, num) values ('4', '2')
insert into Logs (id, num) values ('5', '1')
insert into Logs (id, num) values ('6', '2')
insert into Logs (id, num) values ('7', '2')
```
</details>
<br />

Table: `Logs`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| num         | varchar |
+-------------+---------+
id is the primary key for this table.
id is an autoincrement column.
```

Write an SQL query to find all numbers that appear at least three times consecutively.

Return the result table in any order.

<details>
<summary>Example 1</summary>

```
Input: 
Logs table:
+----+-----+
| id | num |
+----+-----+
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |
+----+-----+
Output: 
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+

Explanation: 1 is the only number that appears consecutively for at least three times.
```
</details>


<details>
<summary>Solution</summary>

```sql
SELECT DISTINCT l1.num AS ConsecutiveNums
FROM 
    Logs l1, 
    Logs l2, 
    Logs l3
WHERE 
    l2.id = l1.id + 1 AND 
    l3.id = l1.id + 2 AND
    l1.num = l2.num AND
    l2.num = l3.num
```
</details>