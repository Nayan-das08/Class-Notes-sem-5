# DBMS Lab Assignment Question 2

## Database Schema
| Entity            | Attributes                                                |
| ----------------- | --------------------------------------------------------- |
| Course_0148       | (cno, cname)                                              |
| Course_fee_0148   | (cno, fp, fees)                                           |
| Course_taken_0148 | (pno, cno, start_date, fp, ampm, perf)                    |
| installment_0148  | (pno, instll_amt, due_date, paid)                         |
| Student_0148      | (pno, pname, add, phno, dob, total_amt, amt_paid, instll) |

---

## Insert Values in the database
```plain
INSERT INTO Student_0148 VALUES
(1001, "Nayan", "Delhi", 725672, "2002-10-04", 28000, 2000.0, "I"),
(1002, "Nehal", "Pune", 623721, "2002-03-06", 2000, 1000.0, "I"),
(1003, "Komal", "Noida", 667417, "2002-05-04", 34000, 12000.0, "I"),
(1004, "Ram", "Trivandrum", 273306, "2002-11-25", 42000, 8000.0, "I"),
(1005, "Shaurya", "Delhi", 527943, "2002-01-16", 22000, 22000, "F"),
(1006, "Keshav", "Chennai", 425653, "2002-09-10", 2000, 2000, "F"),
(1007, "Surya", "Trivandrum", 891627, "2002-09-15", 14000, 5000.0, "I"),
(1008, "Anmol", "Kolkata", 384922, "2002-04-28", 42000, 42000, "F"),
(1009, "Vanshika", "Delhi", 950113, "2002-06-01", 20000, 20000, "F"),
(1010, "Shubham", "Pune", 170043, "2002-02-03", 48000, 25000.0, "I"),
(1011, "Kunal", "Delhi", 313832, "2002-10-27", 42000, 14000.0, "I"),
(1012, "Namit", "Hyderabad", 762890, "2002-08-15", 36000, 36000, "F"),
(1013, "Raghav", "Hyderabad", 424670, "2002-09-17", 20000, 16000.0, "I"),
(1014, "Prakash", "Noida", 572378, "2002-06-30", 42000, 0.0, "I"),
(1015, "Partha", "Hyderabad", 268639, "2002-12-15", 49000, 49000, "F");

INSERT INTO Course_0148 VALUES
(100, "Database Management System"),
(101, "Theory of Computation"),
(102, "Engineering Mathematics"),
(103, "Data Structures"),
(104, "Analysis and Design of Algorithms"),
(105, "Basic Simulation Lab"),
(106, "Engineering Physics"),
(107, "Object Oriented Programming"),
(108, "Artificial Intelligence"),
(109, "Unix");

INSERT INTO Course_fee_0148 VALUES
(100, "F", 27000),
(101, "P", 23000),
(102, "F", 31000),
(103, "P", 16000),
(104, "P", 23000),
(105, "F", 40000),
(106, "P", 27000),
(107, "P", 16000),
(108, "P", 46000),
(109, "F", 49000);

INSERT INTO installment_0148 VALUES
(1001, 400, "2024-10-24", "U"),
(1002, 300, "2024-09-24", "U"),
(1003, 600, "2024-09-27", "U"),
(1004, 700, "2024-12-08", "U"),
(1007, 1500, "2024-11-04", "U"),
(1008, 1800, "2024-06-20", "P"),
(1009, 500, "2024-10-29", "P"),
(1010, 1000, "2024-03-14", "U"),
(1011, 1600, "2024-01-27", "U"),
(1013, 1300, "2024-06-18", "U"),
(1014, 100, "2024-04-19", "U");


INSERT INTO Course_taken_0148 VALUES
(1001, 107, "2022-06-11", "P", "PM", "Average"),
(1002, 105, "2022-05-02", "F", "PM", "Above Avg."),
(1003, 102, "2022-09-06", "F", "PM", "Below Avg."),
(1004, 108, "2022-06-29", "P", "AM", "Above Avg."),
(1005, 105, "2022-05-26", "F", "PM", "Average"),
(1006, 105, "2022-03-03", "F", "PM", "Below Avg."),
(1007, 102, "2022-02-12", "F", "PM", "Below Avg."),
(1008, 105, "2022-10-21", "F", "AM", "Average"),
(1009, 107, "2022-12-19", "P", "AM", "Below Avg."),
(1010, 103, "2022-10-02", "P", "PM", "Below Avg."),
(1011, 103, "2022-04-26", "P", "AM", "Above Avg."),
(1012, 108, "2022-02-03", "P", "PM", "Poor"),
(1013, 109, "2022-02-21", "F", "PM", "Poor"),
(1014, 100, "2022-03-24", "F", "AM", "Above Avg."),
(1015, 104, "2022-02-23", "P", "PM", "Average");
```

---
## Queries
1.  Retrieve name and course no of all the students. 

```plain
SELECT Student_0148.name, Course_taken_0148.course_no 
FROM Student_0148, Course_taken_0148
WHERE Student_0148.prospectus_no = Course_taken_0148.prospectus_no;
```

```plain
mysql> SELECT Student_0148.name, Course_taken_0148.course_no
    -> FROM Student_0148, Course_taken_0148
    -> WHERE Student_0148.prospectus_no = Course_taken_0148.prospectus_no;
+----------+-----------+
| name     | course_no |
+----------+-----------+
| Nayan    | 107       |
| Nehal    | 105       |
| Komal    | 102       |
| Ram      | 108       |
| Shaurya  | 105       |
| Keshav   | 105       |
| Surya    | 102       |
| Anmol    | 105       |
| Vanshika | 107       |
| Shubham  | 103       |
| Kunal    | 103       |
| Namit    | 108       |
| Raghav   | 109       |
| Prakash  | 100       |
| Partha   | 104       |
+----------+-----------+
15 rows in set (0.00 sec)
```

-----------------------------------------------------------
2.  List the names of students who have paid the full amount at the time of admission. 

```plain
SELECT name FROM Student_0148
WHERE installment = "F";
```

```plain
mysql> SELECT name FROM Student_0148
    -> WHERE installment = "F";
+---------+
| name    |
+---------+
| Shaurya |
| Keshav  |
| Namit   |
| Partha  |
+---------+
4 rows in set (0.00 sec)
```
-----------------------------------------------------------
3.  Find the names of students starting with A. 

```plain
SELECT name FROM Student_0148
WHERE name LIKE "A%";
```

```plain
mysql> SELECT name FROM Student_0148
    -> WHERE name LIKE "A%";
+-------+
| name  |
+-------+
| Anmol |
+-------+
1 row in set (0.15 sec)
```
-----------------------------------------------------------
4.  Print the names of students whose total amount is not equal to amount due. 

```plain
SELECT name FROM Student_0148
WHERE total_amt <> amt_paid;
```

```plain
mysql> SELECT name FROM Student_0148
    -> WHERE total_amt <> (total_amt - amt_paid);
+----------+
| name     |
+----------+
| Nayan    |
| Nehal    |
| Komal    |
| Ram      |
| Shaurya  |
| Keshav   |
| Surya    |
| Anmol    |
| Vanshika |
| Shubham  |
| Kunal    |
| Namit    |
| Raghav   |
| Partha   |
+----------+
14 rows in set (0.00 sec)
```
-----------------------------------------------------------
5.  Count the number of students who have joined in current year, current month. 

```plain
SELECT count(prospectus_no) FROM Course_taken_0148
WHERE start_dt LIKE "2022-09-__";
```

```plain
mysql> SELECT count(prospectus_no) FROM Course_taken_0148
    -> WHERE start_dt LIKE "2022-09-__";
+----------------------+
| count(prospectus_no) |
+----------------------+
|                    1 |
+----------------------+
1 row in set (0.00 sec)
```
-----------------------------------------------------------
6.  Determine the maximum and minimum course fees. 

```plain
SELECT min(fees), max(fees) FROM Course_fee_0148;
```

```plain
mysql> SELECT min(fees), max(fees) FROM Course_fee_0148;
+-----------+-----------+
| min(fees) | max(fees) |
+-----------+-----------+
|     16000 |     49000 |
+-----------+-----------+
1 row in set (0.03 sec)
```
-----------------------------------------------------------
7.  Increase the fee of oracle by 50%. 

```plain
UPDATE Course_fee_0148
SET fees = fees + (fees * 0.5)
WHERE course_no = 
    (
        SELECT course_no FROM Course_0148
        WHERE course_name = 'Oracle'
    );
```
-----------------------------------------------------------
8.  Print the details of courses whose fees are between 5000 and 10000. 

```plain
SELECT * FROM Course_fee_0148
WHERE fees BETWEEN 5000 AND 10000;
```

```plain
mysql> SELECT * FROM Course_fee_0148
    -> WHERE fees BETWEEN 5000 AND 10000;
Empty set (0.00 sec)
```
-----------------------------------------------------------
9.  Display the admission date in Date, Month, Year format. 

```plain
SELECT DATE_FORMAT(start_dt,'%D %M %Y') FROM Course_taken_0148;
```

```plain
mysql> select DATE_FORMAT(start_dt,'%D %M %Y') FROM Course_taken_0148;
+----------------------------------+
| DATE_FORMAT(start_dt,'%D %M %Y') |
+----------------------------------+
| 11th June 2022                   |
| 2nd May 2022                     |
| 6th September 2022               |
| 29th June 2022                   |
| 26th May 2022                    |
| 3rd March 2022                   |
| 12th February 2022               |
| 21st October 2022                |
| 19th December 2022               |
| 2nd October 2022                 |
| 26th April 2022                  |
| 3rd February 2022                |
| 21st February 2022               |
| 24th March 2022                  |
| 23rd February 2022               |
+----------------------------------+
15 rows in set (0.00 sec)
```
-----------------------------------------------------------
10. Find out in which course maximum number of students have taken admission. 

```plain
SELECT course_no, count(*) AS "Maximum number of students" FROM course_taken_0148
GROUP BY course_no
HAVING count(*) = 
(
    SELECT max(count) FROM (SELECT course_no, count(*) as count FROM course_taken_0148 GROUP BY course_no) course_count
);
```

```plain
mysql> SELECT course_no, count(*) AS "Maximum number of students" FROM course_taken_0148
    -> GROUP BY course_no
    -> HAVING count(*) =
    -> (
    ->     SELECT max(count) FROM (SELECT course_no, count(*) as count FROM course_taken_0148 GROUP BY course_no) course_count
    -> );
+-----------+----------------------------+
| course_no | Maximum number of students |
+-----------+----------------------------+
| 105       |                          4 |
+-----------+----------------------------+
1 row in set (0.00 sec)
```
-----------------------------------------------------------
11. Change the course_name from Unix to Unix Operating System, 

```plain
UPDATE Course_0148
SET course_name = "Unix Operating System"
WHERE course_name = "Unix";
```

```plain
mysql> SELECT * FROM Course_0148;
+-----------+-----------------------------------+
| course_no | course_name                       |
+-----------+-----------------------------------+
| 100       | Oracle                            |
| 101       | Theory of Computation             |
| 102       | Engineering Mathematics           |
| 103       | Data Structures                   |
| 104       | Analysis and Design of Algorithms |
| 105       | Basic Simulation Lab              |
| 106       | Engineering Physics               |
| 107       | Object Oriented Programming       |
| 108       | Artificial Intelligence           |
| 109       | Unix Operating System             |
+-----------+-----------------------------------+
10 rows in set (0.00 sec)
```
-----------------------------------------------------------
12. Display the admission date in DD-MONTH-YYYY format. 

```plain
SELECT DATE_FORMAT(start_dt, '%d-%m-%Y') from Course_taken_0148;
```

```plain
mysql> SELECT DATE_FORMAT(start_dt, '%d-%m-%Y') from Course_taken_0148;
+-----------------------------------+
| DATE_FORMAT(start_dt, '%d-%m-%Y') |
+-----------------------------------+
| 11-06-2022                        |
| 02-05-2022                        |
| 06-09-2022                        |
| 29-06-2022                        |
| 26-05-2022                        |
| 03-03-2022                        |
| 12-02-2022                        |
| 21-10-2022                        |
| 19-12-2022                        |
| 02-10-2022                        |
| 26-04-2022                        |
| 03-02-2022                        |
| 21-02-2022                        |
| 24-03-2022                        |
| 23-02-2022                        |
+-----------------------------------+
15 rows in set (0.00 sec)
```
-----------------------------------------------------------
13. Get the sum of amount to be collected from students in this month. 

```plain
SELECT sum(installment_amt) from installment_0148
WHERE due_dt LIKE "____-09-__";
```

```plain
mysql> SELECT sum(installment_amt) from installment_0148
    -> WHERE due_dt LIKE "____-09-__";
+----------------------+
| sum(installment_amt) |
+----------------------+
|               900.00 |
+----------------------+
1 row in set (0.00 sec)

```
-----------------------------------------------------------
14. Find out in which course the maximum number of students have taken admission in the current month. 

```plain
SELECT course_no, count(*) FROM Course_taken_0148
WHERE start_dt like "____-09-__"
GROUP BY course_no
HAVING count(*) = 
(
    SELECT max(count) FROM 
    (
        SELECT course_no as course, count(*) as count FROM Course_taken_0148
        WHERE start_dt like "____-09-__"
        GROUP BY course_no
    ) new
);
```

```plain
mysql> SELECT course_no, count(*) FROM Course_taken_0148
    -> WHERE start_dt like "____-09-__"
    -> GROUP BY course_no
    -> HAVING count(*) =
    -> (
    ->     SELECT max(count) FROM
    ->     (
    ->         SELECT course_no as course, count(*) as count FROM Course_taken_0148
    ->         WHERE start_dt like "____-09-__"
    ->         GROUP BY course_no
    ->     ) new
    -> );
+-----------+----------+
| course_no | count(*) |
+-----------+----------+
| 102       |        1 |
+-----------+----------+
1 row in set (0.00 sec)
```

-----------------------------------------------------------
15. Select the students who have not yet paid full amount of fees

```plain
SELECT * FROM Student_0148
WHERE total_amt <> amt_paid;
```

```plain
mysql> SELECT * FROM Student_0148
    -> WHERE total_amt <> amt_paid;
+---------------+---------+------------+----------+------------+-----------+----------+-------------+
| prospectus_no | name    | address    | phone_no | D_O_B      | total_amt | amt_paid | installment |
+---------------+---------+------------+----------+------------+-----------+----------+-------------+
|          1001 | Nayan   | Delhi      |   725672 | 2002-10-04 |  28000.00 |  2000.00 | I           |
|          1002 | Nehal   | Pune       |   623721 | 2002-03-06 |   2000.00 |  1000.00 | I           |
|          1003 | Komal   | Noida      |   667417 | 2002-05-04 |  34000.00 | 12000.00 | I           |
|          1004 | Ram     | Trivandrum |   273306 | 2002-11-25 |  42000.00 |  8000.00 | I           |
|          1007 | Surya   | Trivandrum |   891627 | 2002-09-15 |  14000.00 |  5000.00 | I           |
|          1010 | Shubham | Pune       |   170043 | 2002-02-03 |  48000.00 | 25000.00 | I           |
|          1011 | Kunal   | Delhi      |   313832 | 2002-10-27 |  42000.00 | 14000.00 | I           |
|          1013 | Raghav  | Hyderabad  |   424670 | 2002-09-17 |  20000.00 | 16000.00 | I           |
|          1014 | Prakash | Noida      |   572378 | 2002-06-30 |  42000.00 |     0.00 | I           |
+---------------+---------+------------+----------+------------+-----------+----------+-------------+
9 rows in set (0.00 sec)
```
-----------------------------------------------------------
