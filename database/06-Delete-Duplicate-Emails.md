## Delete Duplicate Emails

Write a SQL query to delete all duplicate email entries in a table named Person, keeping only unique emails based on its smallest Id.

|Id|Email|
|:-|:-|
|1|john@example.com|
|2|bob@example.com|
|3|john@example.com|

Id is the primary key column for this table.
For example, after running your query, the above Person table should have the following rows:

|Id|Email|
|:-|:-|
|1|john@example.com|
|2|bob@example.com|

**解法**

错误示范

```mysql
DELETE FROM Person WHERE Id NOT IN (
  SELECT Id FROM Person GROUP BY Email ORDER BY Id ASC 
)
```
现在才知道这样会引起语法错误，而且GROUP BY 和 ORDER BY 同时用，上面的例子ORDER BY其实没有效果。

有其他提交也是类似的思路，正确的应该使用MIN函数：

```mysql
DELETE FROM Person
WHERE Id NOT IN (
  SELECT * FROM (
    SELECT MIN(Id) FROM Person GROUP BY Email 
  ) AS temp
)
```
参考答案

```mysql
DELETE p1 FROM Person p1,
    Person p2
WHERE
    p1.Email = p2.Email AND p1.Id > p2.Id
```