%%[[_Lab Files]]%%
%%#lab/dbms%%
# Experiment 4
To learn and implement SQL Clauses - ***GROUP BY*** and ***HAVING***; and carry out ***Equi Join*** on two tables.

---
## GROUP BY Clause
- The **GROUP BY** statement groups rows that have the same values into summary rows, like "find the number of customers in each country".
- The **GROUP BY** statement is often used with aggregate functions (*count(), max(), min(), sum(), avg()*) to group the result-set by one or more columns.

**Syntax:**
```plain
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)  
HAVING condition  
ORDER BY column_name(s);
```
---

## HAVING Clause
- The **HAVING** clause was added to SQL because the WHERE keyword cannot be used with aggregate functions.

**Syntax:**
```plain
SELECT column_name(s)
FROM table_name  
WHERE condition
GROUP BY column_name(s)  
ORDER BY column_name(s);
```
---
## SQL Equi Join 
- SQL EQUI JOIN performs a JOIN against equality or matching column(s) values of the associated tables. 
- An equal sign (=) is used as comparison operator in the where clause to refer equality.
- You may also perform EQUI JOIN by using JOIN keyword followed by ON keyword

**Syntax:**
```plain
SELECT column_name(s)
FROM table1, table2  
WHERE table1.column_name = table2.column_name;
```

```plain
SELECT column_name(s)
FROM table1 JOIN table2  
ON table1.column_name = table2.column_name;
```
---
## Output
1. GROUP BY Clause
```plain
mysql> SELECT count(c_id), country from customer
    -> GROUP BY country;
+-------------+---------+
| count(c_id) | country |
+-------------+---------+
|           4 | India   |
|           2 | Canada  |
|           2 | France  |
+-------------+---------+
3 rows in set (0.12 sec)
```
---
2. HAVING Clause
```plain
mysql> SELECT count(c_id), country from customer
    -> GROUP BY country
    -> HAVING count(c_id) > 2;
+-------------+---------+
| count(c_id) | country |
+-------------+---------+
|           4 | India   |
+-------------+---------+
1 row in set (0.03 sec)
```
---
3. SQL Equi Join
```plain
mysql> SELECT orders.Order_no, orders.Customer_id, 
       customer.c_name, orders.Order_status
    -> FROM customer, orders
    -> WHERE customer.c_id = orders.Customer_id
    -> ORDER BY customer.c_id;
+----------+-------------+----------+-----------------+
| Order_no | Customer_id | c_name   | Order_status    |
+----------+-------------+----------+-----------------+
|     1236 |           2 | Pragnya  | Order Cancelled |
|     1237 |           3 | Adersh   | Delivered       |
|     1235 |           4 | Yash     | Dispatched      |
|     1234 |           7 | Jaisurya | Delivered       |
|     1238 |           9 | Shivansh | Delivered       |
+----------+-------------+----------+-----------------+
5 rows in set (0.00 sec)
```