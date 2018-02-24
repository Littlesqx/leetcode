## Swap Salary

```
Given a table salary, such as the one below, that has m=male and f=female values. Swap all f and m values (i.e., change all f values to m and vice versa) with a single update query and no intermediate temp table.

For example:

| id | name | sex | salary |
|----|------|-----|--------|
| 1  | A    | m   | 2500   |
| 2  | B    | f   | 1500   |
| 3  | C    | m   | 5500   |
| 4  | D    | f   | 500    |

After running your query, the above salary table should have the following rows:

| id | name | sex | salary |
|----|------|-----|--------|
| 1  | A    | f   | 2500   |
| 2  | B    | m   | 1500   |
| 3  | C    | f   | 5500   |
| 4  | D    | m   | 500    |
```

1# 使用 `IF(expr1, expr2, expr3)`

> 如果 `expr1` 是 `TRUE(expr1 <> 0 and expr1 <> NULL)` ，则 `IF()` 的返回值为 `expr2` ; 否则返回值则为 `expr3` 。

```mysql
UPDATE salary SET sex = IF(sex = 'm', 'f', 'm')
```

2# 使用 `CASE...WHEN...`

```mysql
UPDATE salary SET sex = CASE sex
    WHEN 'm' THEN 'f'
    ELSE 'm'
END
```

3# 使用 `XOR` ( a xor b xor a = b )

```mysql
UPDATE salary SET sex = CHAR(ASCII(sex) ^ ASCII('m') ^ ASCII('f'))
```


