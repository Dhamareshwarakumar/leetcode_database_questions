## Rising Temperature

<details>
<summary>Schema</summary>

```sql
Create table If Not Exists Weather (id int, recordDate date, temperature int)
Truncate table Weather
insert into Weather (id, recordDate, temperature) values ('1', '2015-01-01', '10')
insert into Weather (id, recordDate, temperature) values ('2', '2015-01-02', '25')
insert into Weather (id, recordDate, temperature) values ('3', '2015-01-03', '20')
insert into Weather (id, recordDate, temperature) values ('4', '2015-01-04', '30')
```
</details>
<br />

Table: `Weather`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| recordDate    | date    |
| temperature   | int     |
+---------------+---------+
id is the primary key for this table.
This table contains information about the temperature on a certain day.
```

Write an SQL query to find all dates' Id with higher temperatures compared to its previous dates (yesterday).

Return the result table in any order.

<details>
<summary>Example 1</summary>

```
Input: 
Weather table:
+----+------------+-------------+
| id | recordDate | temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+
Output: 
+----+
| id |
+----+
| 2  |
| 4  |
+----+
Explanation: 
In 2015-01-02, the temperature was higher than the previous day (10 -> 25).
In 2015-01-04, the temperature was higher than the previous day (20 -> 30).
```
</details>


<details>
<summary>Solution 1</summary>

```sql
SELECT id from Weather w1 WHERE temperature > (select temperature from weather where recordDate = DATE_SUB(w1.recordDate, INTERVAL 1 DAY))
```
</details>

<details>
<summary>Solution 2</summary>

```sql
SELECT w2.id from Weather w1 JOIN Weather w2 ON DATEDIFF(w2.recordDate, w1.recordDate) = 1 AND w2.temperature > w1.temperature 
```
</details>