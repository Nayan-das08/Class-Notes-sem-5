%%[[_Lab Files]]%%
%%#lab/dbms%% 
# Experiment 3
To learn SQL ***aggregate functions***, ***order by*** keyword, ***like*** operator, ***Wildcards***, ***between*** operator and ***SQL Aliases***.

---
## SQL Aggregate Functions
They return a single value, calculated from values in a column.

**Useful aggregate functions:**

| Function | Role                       |
| -------- | -------------------------- |
| Avg( )   | Returns the average value  |
| Count( ) | Returns the number of rows |
| Min( )   | Returns the smallest value |
| Max( )   | Returns the largest value  |
| Sum( )   | Returns the sum            |

### SQL ORDER BY keyword
- Used to sort the result-set by one or more columns.
- The ORDER BY keyword sorts the records in ascending order by default. 
- To sort the records in a descending order, you can use the **DESC** keyword.

**Syntax:**
```plain
SELECT column_name, column_name
FROM table_name
ORDER BY column_name ASC|DESC, column_name ASC|DESC;
```
---
### SQL LIKE Operator 
- The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.

**Syntax:**
```plain
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern;
```
---
### SQL Wildcards
- A wildcard character can be used to substitute for any other character(s) in a string. 
- Wildcard characters are used with the SQL **LIKE** operator. 
- Wildcards are used to search for data within the table.

**Wildcard Characters in MySQL**

| Symbol | Description                        | Example                             |
|:------:| ---------------------------------- | ----------------------------------- |
|   %    | Represents zero or more characters | bl% finds bl, black, blue, and blob |
|   -    | Represents a single character      | h_t finds hot, hat, and hit         |

---
### SQL BETWEEN operator  
- Selects values within a range. The values can be numbers, text, or dates.

**Syntax:**
```plain
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```
---
### SQL Aliases 
- SQL aliases are used to give a database table, or a column in a table, a temporary name. 
- Basically, aliases are created to make column names more readable.

**Syntax:**
```plain
SELECT column_name AS alias_name
FROM table_name;
```
---

## Outputs
Implementing aggregate functions from the following table :-
```plain
mysql> SELECT * FROM employee;
+-------+----------+--------+--------+----------+------------+
| empid | empname  | salary | gender | dept_no  | doj        |
+-------+----------+--------+--------+----------+------------+
|   100 | Shubham  |  56325 | Male   | IT       | 2022-01-15 |
|   101 | Prapti   |  59500 | Female | IT       | 2022-01-20 |
|   102 | Nayan    |  51500 | Male   | HR       | 2022-01-20 |
|   103 | Jaisurya |  51200 | Male   | Medical  | 2022-03-10 |
|   104 | Pragnya  |  51100 | Female | Accounts | 2021-05-12 |
|   105 | Shruti   |  52660 | Female | IT       | 2023-08-26 |
|   106 | Dikhsha  |  54660 | Female | Accounts | 2023-04-22 |
+-------+----------+--------+--------+----------+------------+
7 rows in set (0.00 sec)
```

<div style="page-break-after: always; visibility: hidden">
\pagebreak
</div>

1. min()
```plain
mysql> SELECT min(salary) FROM employee;
+-------------+
| min(salary) |
+-------------+
|       51100 |
+-------------+
1 row in set (0.04 sec)

mysql> SELECT * FROM employee
    -> WHERE salary = (SELECT min(salary) FROM employee);
+-------+---------+--------+--------+----------+------------+
| empid | empname | salary | gender | dept_no  | doj        |
+-------+---------+--------+--------+----------+------------+
|   104 | Pragnya |  51100 | Female | Accounts | 2021-05-12 |
+-------+---------+--------+--------+----------+------------+
1 row in set (0.10 sec)
```
---
2. max()
```plain
mysql> SELECT max(salary) FROM employee;
+-------------+
| max(salary) |
+-------------+
|       59500 |
+-------------+
1 row in set (0.00 sec)
```
---
3. sum()
```plain
mysql> SELECT sum(salary) FROM employee;
+-------------+
| sum(salary) |
+-------------+
|      376945 |
+-------------+
1 row in set (0.00 sec)
```
---
4. avg()
```plain
mysql> SELECT avg(salary) FROM employee;
+-------------+
| avg(salary) |
+-------------+
|  53849.2857 |
+-------------+
1 row in set (0.03 sec)
```
---
5. count()
```plain
mysql> SELECT count(*) FROM employee;
+----------+
| count(*) |
+----------+
|        7 |
+----------+
1 row in set (0.20 sec)

mysql> SELECT (sum(salary))/count(*) AS "avg(sal)" FROM employee;
+------------+
| avg(sal)   |
+------------+
| 53849.2857 |
+------------+
1 row in set (0.00 sec)

mysql> SELECT count(DISTINCT dept_no) FROM employee;
+-------------------------+
| count(DISTINCT dept_no) |
+-------------------------+
|                       4 |
+-------------------------+
1 row in set (0.00 sec)

mysql> SELECT count(*) FROM employee
    -> WHERE gender = "Male";
+----------+
| count(*) |
+----------+
|        3 |
+----------+
1 row in set (0.00 sec)
```
---
6. SQL ORDER BY keyword
```plain
mysql> SELECT * FROM employee
    -> ORDER BY empid DESC;
+-------+----------+--------+--------+----------+------------+
| empid | empname  | salary | gender | dept_no  | doj        |
+-------+----------+--------+--------+----------+------------+
|   106 | Dikhsha  |  54660 | Female | Accounts | 2023-04-22 |
|   105 | Shruti   |  52660 | Female | IT       | 2023-08-26 |
|   104 | Pragnya  |  51100 | Female | Accounts | 2021-05-12 |
|   103 | Jaisurya |  51200 | Male   | Medical  | 2022-03-10 |
|   102 | Nayan    |  51500 | Male   | HR       | 2022-01-20 |
|   101 | Prapti   |  59500 | Female | IT       | 2022-01-20 |
|   100 | Shubham  |  56325 | Male   | IT       | 2022-01-15 |
+-------+----------+--------+--------+----------+------------+
7 rows in set (0.00 sec)

mysql> SELECT * FROM employee
    -> ORDER BY empname;
+-------+----------+--------+--------+----------+------------+
| empid | empname  | salary | gender | dept_no  | doj        |
+-------+----------+--------+--------+----------+------------+
|   106 | Dikhsha  |  54660 | Female | Accounts | 2023-04-22 |
|   103 | Jaisurya |  51200 | Male   | Medical  | 2022-03-10 |
|   102 | Nayan    |  51500 | Male   | HR       | 2022-01-20 |
|   104 | Pragnya  |  51100 | Female | Accounts | 2021-05-12 |
|   101 | Prapti   |  59500 | Female | IT       | 2022-01-20 |
|   105 | Shruti   |  52660 | Female | IT       | 2023-08-26 |
|   100 | Shubham  |  56325 | Male   | IT       | 2022-01-15 |
+-------+----------+--------+--------+----------+------------+
7 rows in set (0.00 sec)
```
---
7. SQL BETWEEN keyword
```plain
mysql> SELECT * FROM employee
    -> WHERE empid BETWEEN 100 AND 103;
+-------+----------+--------+--------+---------+------------+
| empid | empname  | salary | gender | dept_no | doj        |
+-------+----------+--------+--------+---------+------------+
|   100 | Shubham  |  56325 | Male   | IT      | 2022-01-15 |
|   101 | Prapti   |  59500 | Female | IT      | 2022-01-20 |
|   102 | Nayan    |  51500 | Male   | HR      | 2022-01-20 |
|   103 | Jaisurya |  51200 | Male   | Medical | 2022-03-10 |
+-------+----------+--------+--------+---------+------------+
4 rows in set (0.00 sec)

mysql> SELECT * FROM employee
    -> WHERE empname BETWEEN "A" AND "L";
+-------+----------+--------+--------+----------+------------+
| empid | empname  | salary | gender | dept_no  | doj        |
+-------+----------+--------+--------+----------+------------+
|   103 | Jaisurya |  51200 | Male   | Medical  | 2022-03-10 |
|   106 | Dikhsha  |  54660 | Female | Accounts | 2023-04-22 |
+-------+----------+--------+--------+----------+------------+
2 rows in set (0.00 sec)
```
---
8. SQL Aliases
```plain
mysql> SELECT empid AS employee_ID FROM employee;
+-------------+
| employee_ID |
+-------------+
|         100 |
|         101 |
|         102 |
|         103 |
|         104 |
|         105 |
|         106 |
+-------------+
7 rows in set (0.00 sec)

mysql> SELECT max(salary) AS MAX_Salary FROM employee;
+------------+
| MAX_Salary |
+------------+
|      59500 |
+------------+
1 row in set (0.00 sec)
```
---
9. SQL LIKE operator and wildcard characters
```plain
mysql> SELECT * FROM employee
    -> WHERE empname LIKE "%i%";
+-------+----------+--------+--------+----------+------------+
| empid | empname  | salary | gender | dept_no  | doj        |
+-------+----------+--------+--------+----------+------------+
|   101 | Prapti   |  59500 | Female | IT       | 2022-01-20 |
|   103 | Jaisurya |  51200 | Male   | Medical  | 2022-03-10 |
|   105 | Shruti   |  52660 | Female | IT       | 2023-08-26 |
|   106 | Dikhsha  |  54660 | Female | Accounts | 2023-04-22 |
+-------+----------+--------+--------+----------+------------+
4 rows in set (0.02 sec)

mysql> SELECT * FROM employee
    -> WHERE doj LIKE "2022-%";
+-------+----------+--------+--------+---------+------------+
| empid | empname  | salary | gender | dept_no | doj        |
+-------+----------+--------+--------+---------+------------+
|   100 | Shubham  |  56325 | Male   | IT      | 2022-01-15 |
|   101 | Prapti   |  59500 | Female | IT      | 2022-01-20 |
|   102 | Nayan    |  51500 | Male   | HR      | 2022-01-20 |
|   103 | Jaisurya |  51200 | Male   | Medical | 2022-03-10 |
+-------+----------+--------+--------+---------+------------+
4 rows in set (0.00 sec)
```
