## Employees Earning More Than Their Managers
The Employee table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id.

|Id|Name|Salary|ManagerId|
|:-|:-|:-|:-|
|1|Joe|70000|3|
|2|Henry|80000|4|
|3|Sam|60000|NULL|
|4|Max|90000|NULL|

Given the Employee table, write a SQL query that finds out employees who earn more than their managers. For the above table, Joe is the only employee who earns more than his manager.

|Employee|
|:-|
|Joe|

**解法**

```mysql
SELECT Name AS Employee from (
    SELECT a.Name, a.Salary, b.Salary AS ManagerSalary FROM Employee a INNER JOIN Employee b ON a.ManagerId = b.Id
) c WHERE c.Salary > c.ManagerSalary
```
参考答案：
```mysql
SELECT a.Name AS Employee FROM 
Employee a 
INNER JOIN Employee b ON a.ManagerId = b.Id AND a.Salary > b.Salary
```
显然自己的方法多余了。。。