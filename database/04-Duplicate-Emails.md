## Duplicate Emails

Write a SQL query to find all duplicate emails in a table named Person.

|Id|Email|
|:-|:-|
|1|a@b.com|
|2|c@d.com|
|3|a@b.com|

For example, your query should return the following for the above table:

|Email|
|:-|
|a@b.com|

**解法**

容易想到group by和子查询

```mysql
SELECT Email FROM (
  SELECT Email, count(Email) AS num FROM Person GROUP BY Email
) a WHERE a.num > 1
```

参考答案还有一个HAVEING的用法

```mysql
SELECT Email FROM Person GROUP BY Email HAVING count(Email) > 1
```
