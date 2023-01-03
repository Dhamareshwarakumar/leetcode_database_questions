## Delete Duplicate Emails

<details>
<summary>Schema</summary>

```sql
Create table If Not Exists Person (Id int, Email varchar(255))
Truncate table Person
insert into Person (id, email) values ('1', 'john@example.com')
insert into Person (id, email) values ('2', 'bob@example.com')
insert into Person (id, email) values ('3', 'john@example.com')
```
</details>
<br />

Table: `Person`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| id          | int     |
| email       | varchar |
+-------------+---------+
id is the primary key column for this table.
Each row of this table contains an email. The emails will not contain uppercase letters.
```

Write an SQL query to delete all the duplicate emails, keeping only one unique email with the smallest `id`. Note that you are supposed to write a `DELETE` statement and not a `SELECT` one.

After running your script, the answer shown is the `Person` table. The driver will first compile and run your piece of code and then show the `Person` table. The final order of the `Person` table does not matter.

<details>
<summary>Example 1</summary>

```
Input: 
Person table:
+----+------------------+
| id | email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
Output: 
+----+------------------+
| id | email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+
Explanation: john@example.com is repeated two times. We keep the row with the smallest Id = 1.
```
</details>


<details>
<summary>Solution 1</summary>

```sql
DELETE FROM Person 
WHERE id NOT IN (
    SELECT min_id FROM (
        SELECT MIN(id) as min_id FROM Person 
        GROUP BY email
    ) p
);
```
</details>

<details>
<summary>Solution 2</summary>

```sql
DELETE p2 FROM Person p1 JOIN Person p2 
ON p2.Email = p1.Email WHERE p2.Id > p1.Id;
```
</details>