## Second Highest Salary

Write a SQL query to get the second highest salary from the Employee table.

|Id|Salary|
|:-|:-|
|1|100|
|2|200|
|3|300|

For example, given the above Employee table, the query should return 200 as the second highest salary. If there is no second highest salary, then the query should return null.

|SecondHighestSalary|
|:-|
|200|

**关键**
- second highest
- If there is no second highest salary, then the query should return null.

**解法：**

```mysql
SELECT IFNULL((
    SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT 1, 1
), NULL) AS SecondHighestSalary;
```

**心得**

参考了答案，不知道有IFNULL函数，直接 SELECT查询结果AS也让我惊了。第二高也没有留意到要用DISTINCT。