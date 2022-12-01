%%[[_Lab Files]]%%
%%#lab/dbms%%
# DBMS Lab Assignment Question 3
## Database Schema
| Entity     | Attributes                                                          |
| ---------- | ------------------------------------------------------------------- |
| Department | (dept_no, dept_name)                                                | 
| Employee   | (e_id, e_name, salary, hiredate, loc, mgr_eid, job, grade, dept_no) |

```plain
CREATE TABLE Department
(
	dept_no 	char(4)		PRIMARY KEY,
	dept_name 	varchar(50)	NOT NULL
);
```
---
```plain
CREATE TABLE Employee
(
	e_ID 		char(4)			PRIMARY KEY, 
	e_Name 		varchar(20)		NOT NULL, 
	salary		integer(20)		NOT NULL, 
	hiredate	date 			NOT NULL, 
	loc			varchar(20), 
	mgr_eid		char(4)			NOT NULL, 
	job			varchar(50)		NOT NULL, 
	grade		char(1)			NOT NULL, 
	dept_no		char(4)			NOT NULL,
	FOREIGN KEY (dept_No) REFERENCES Department(dept_no)
);
```
---

## Insert values in the database
```plain
INSERT INTO Department VALUES
("D001", "Management"),				|	CEO, COO, CFO
("D002", "Administration"),			|	Office Administrator, Receptionist
("D003", "Human Resources"),		|	HR Recuiter, Coordinator
("D004", "Legal"),					|	Legal Advisor
("D005", "Finance"),				|	Finance Manager
("D006", "Marketing"),				|	Marketing Manager
("D007", "Logisitics"),				|	Warehouse Manager, Logistics Executive
("D008", "Customer Service"),		|	Customer Service Representative, Executive
("D009", "Quality Assurance"),		|	Quality Assurance Manager, Officer
("D010", "Production"),				|	Production Supervisor, Engineer
("D011", "Information Technology"),	|	IT Engineer
("D012", "Sales"),					|	Salesperson, Executive
("D013", "Systems"),				|	System Administrator

INSERT INTO Employee VALUES
("E001", "Nayan", 19000, "2005-01-30", "Trivandrum", "E006", "Salesperson", "E", "D012"),
("E002", "Nehal", 11000, "2011-08-11", "Delhi", "E005", "Finance Manager", "B", "D005"),
("E003", "Komal", 2000, "2016-05-18", "Hyderabad", "E005", "CFO", "D", "D001"),
("E004", "Ram", 78000, "2017-05-09", "Chennai", "E007", "Production Supervisor", "A", "D010"),
("E005", "Shaurya", 45000, "2007-05-03", "Kolkata", "E003", "CTO", "A", "D001"),
("E006", "Keshav", 75000, "2002-06-12", "Kolkata", "E009", "Salesperson", "C", "D012"),
("E007", "Surya", 54000, "2017-11-12", "Delhi", "E006", "Recruiter", "D", "D003"),
("E008", "Anmol", 68000, "2006-10-13", "Hyderabad", "E006", "Legal Advisor", "B", "D004"),
("E009", "Vanshika", 63000, "2017-04-15", "Hyderabad", "E002", "Office Administrator", "A", "D002"),
("E010", "Shubham", 92000, "2011-07-17", "Kolkata", "E003", "HR Recuiter", "B", "D003"),
("E011", "Kunal", 44000, "2002-05-27", "Chennai", "E010", "Receptionist", "B", "D002"),
("E012", "Namit", 5000, "2003-02-28", "Trivandrum", "E002", "Production Engineer", "E", "D010"),
("E013", "Raghav", 90000, "2012-07-22", "Hyderabad", "E010", "Warehouse Manager", "D", "D007"),
("E014", "Prakash", 88000, "2018-09-16", "Kolkata", "E003", "Customer Service Representative", "B", "D008"),
("E015", "Partha", 33000, "2015-10-16", "Trivandrum", "E008", "HR Recuiter", "A", "D003"),
("E016", "Adersh", 75000, "2001-09-14", "Trivandrum", "E001", "Salesperson", "C", "D012"),
("E017", "Pragnya", 4000, "2020-02-02", "Chennai", "E010", "Finance Manager", "B", 	"D005"),
("E018", "Jaisurya", 100000, "2004-12-22", "Noida", "E009", "CEO", "E", "D001"),
("E019", "Shivansh", 12000, "2019-02-06", "Hyderabad", "E002", "Legal Advisor", "A", "D004"),
("E020", "Yash", 72000, "2007-05-24", "Chennai", "E006", "Salesperson", "E", "D012")
("E021", "Prapti", 19000, "2001-03-18", "Trivandrum", "E005", "System Administrator", "C", "D013"),
("E022", "Vansh", 39000, "2011-10-05", "Pune", "E001", "System Administrator", "B", "D013");
```
---

## Queries
1.	Display each employee name and hiredate of systems department.

```plain
SELECT e_name, hiredate FROM Employee
WHERE dept_no = 
(
	SELECT dept_no FROM Department 
	WHERE dept_name = "Systems"
);
```

```plain
mysql> SELECT e_name, hiredate FROM Employee
    -> WHERE dept_no =
    -> (
    ->  SELECT dept_no FROM Department
    ->  WHERE dept_name = "Systems"
    -> );
+--------+------------+
| e_name | hiredate   |
+--------+------------+
| Prapti | 2001-03-18 |
| Vansh  | 2011-10-05 |
+--------+------------+
2 rows in set (0.00 sec)
```
--------------------------------------------------------------
2.	Write query to calculate length of service of each employee.

```plain
SELECT e_name, TIMESTAMPDIFF(YEAR, hiredate, CURDATE()) AS "Years of service" FROM Employee;
```

```plain
mysql> SELECT e_name, TIMESTAMPDIFF(YEAR, hiredate, CURDATE())
       AS "Years of service" FROM Employee;
+----------+------------------+
| e_name   | Years of service |
+----------+------------------+
| Nayan    |               17 |
| Nehal    |               11 |
| Komal    |                6 |
| Ram      |                5 |
| Shaurya  |               15 |
| Keshav   |               20 |
| Surya    |                4 |
| Anmol    |               15 |
| Vanshika |                5 |
| Shubham  |               11 |
| Kunal    |               20 |
| Namit    |               19 |
| Raghav   |               10 |
| Prakash  |                4 |
| Partha   |                6 |
| Adersh   |               21 |
| Pragnya  |                2 |
| Jaisurya |               17 |
| Shivansh |                3 |
| Yash     |               15 |
| Prapti   |               21 |
| Vansh    |               10 |
+----------+------------------+
22 rows in set (0.00 sec)
```
--------------------------------------------------------------
3.	Find the second maximum salary of all employees.

```plain
SELECT e_name, salary FROM Employee ORDER BY salary DESC limit 1,1;
```

```plain
mysql> SELECT e_name, salary FROM Employee ORDER BY salary DESC LIMIT 1,1;
+---------+--------+
| e_name  | salary |
+---------+--------+
| Shubham |  92000 |
+---------+--------+
1 row in set (0.00 sec)
```
--------------------------------------------------------------
4.	Display all employee name and department name in department name order. 

```plain
SELECT Employee.e_name, Department.dept_name FROM Employee, Department
WHERE Employee.dept_no = Department.dept_no
ORDER BY dept_name;
```

```plain
mysql> SELECT Employee.e_name, Department.dept_name FROM Employee, Department
    -> WHERE Employee.dept_no = Department.dept_no
    -> ORDER BY dept_name;
+----------+------------------+
| e_name   | dept_name        |
+----------+------------------+
| Vanshika | Administration   |
| Kunal    | Administration   |
| Prakash  | Customer Service |
| Nehal    | Finance          |
| Pragnya  | Finance          |
| Surya    | Human Resources  |
| Shubham  | Human Resources  |
| Partha   | Human Resources  |
| Anmol    | Legal            |
| Shivansh | Legal            |
| Raghav   | Logisitics       |
| Komal    | Management       |
| Shaurya  | Management       |
| Jaisurya | Management       |
| Ram      | Production       |
| Namit    | Production       |
| Nayan    | Sales            |
| Keshav   | Sales            |
| Adersh   | Sales            |
| Yash     | Sales            |
| Prapti   | Systems          |
| Vansh    | Systems          |
+----------+------------------+
22 rows in set (0.00 sec)
```
--------------------------------------------------------------
5.	Find the name of lowest paid employee for each manager. 

```plain
SELECT e_name, Employee.mgr_eid AS manager_id, salary, 
min_sal AS "Min. salary for this manager" FROM Employee,
(SELECT mgr_eid, min(salary) AS min_sal FROM Employee 
GROUP BY mgr_eid) manager_min_sal
WHERE Employee.mgr_eid = manager_min_sal.mgr_eid
AND salary = min_sal;
```

```plain
mysql> SELECT e_name, Employee.mgr_eid AS manager_id, salary, 
    -> min_sal AS "Min. salary for this manager" FROM Employee,
    -> (SELECT mgr_eid, min(salary) AS min_sal FROM Employee 
    ->  GROUP BY mgr_eid) manager_min_sal
    -> WHERE Employee.mgr_eid = manager_min_sal.mgr_eid
    -> AND salary = min_sal;
+---------+------------+--------+------------------------------+
| e_name  | manager_id | salary | Min. salary for this manager |
+---------+------------+--------+------------------------------+
| Nayan   | E006       |  19000 |                        19000 |
| Komal   | E005       |   2000 |                         2000 |
| Ram     | E007       |  78000 |                        78000 |
| Shaurya | E003       |  45000 |                        45000 |
| Keshav  | E009       |  75000 |                        75000 |
| Namit   | E002       |   5000 |                         5000 |
| Partha  | E008       |  33000 |                        33000 |
| Pragnya | E010       |   4000 |                         4000 |
| Vansh   | E001       |  39000 |                        39000 |
+---------+------------+--------+------------------------------+
9 rows in set (0.00 sec)
```
--------------------------------------------------------------
6.	Display the department that has no employee.

```plain
SELECT dept_no, dept_name FROM Department
WHERE dept_no NOT IN 
(
	SELECT dept_no from Employee
	GROUP BY dept_no
);
```

```plain
mysql> SELECT dept_no, dept_name FROM Department
    -> WHERE dept_no NOT IN
    -> (
    ->  SELECT dept_no from Employee
    ->  GROUP BY dept_no
    -> );
+---------+------------------------+
| dept_no | dept_name              |
+---------+------------------------+
| D006    | Marketing              |
| D009    | Quality Assurance      |
| D011    | Information Technology |
+---------+------------------------+
3 rows in set (0.00 sec)
```
--------------------------------------------------------------
7.	Find the employees who earn the maximum salary in each job type. Sort in descending order of salary. 

```plain
SELECT job, max(salary) FROM employee 
GROUP BY job
ORDER BY max(salary) DESC;
```

```plain
mysql> SELECT job, max(salary) FROM employee
    -> GROUP BY job
    -> ORDER BY max(salary) DESC;
+---------------------------------+-------------+
| job                             | max(salary) |
+---------------------------------+-------------+
| CEO                             |      100000 |
| HR Recuiter                     |       92000 |
| Warehouse Manager               |       90000 |
| Customer Service Representative |       88000 |
| Production Supervisor           |       78000 |
| Salesperson                     |       75000 |
| Legal Advisor                   |       68000 |
| Office Administrator            |       63000 |
| Recruiter                       |       54000 |
| CTO                             |       45000 |
| Receptionist                    |       44000 |
| System Administrator            |       39000 |
| Finance Manager                 |       11000 |
| Production Engineer             |        5000 |
| CFO                             |        2000 |
+---------------------------------+-------------+
15 rows in set (0.00 sec)
```
--------------------------------------------------------------
8.	In which year did most people joined the company? Display the year and number of employees. 

```plain
SELECT date_format(hiredate, "%Y") as year, count(*) as "# people hired" FROM Employee
GROUP BY year
HAVING count(*) = 
(
	SELECT max(count) FROM
	(
		SELECT date_format(hiredate, "%Y") as year, count(*) as count FROM Employee 
		GROUP BY year
	) year_count
);
```

```plain
mysql> SELECT date_format(hiredate, "%Y") as year, count(*) as "# people hired" 
    -> FROM Employee
    -> GROUP BY year
    -> HAVING count(*) =
    -> (
    ->  SELECT max(count) FROM
    ->  (
    ->          SELECT date_format(hiredate, "%Y") as year, count(*) as count 
    ->          FROM Employee
    ->          GROUP BY year
    ->  ) year_count
    -> );
+------+----------------+
| year | # people hired |
+------+----------------+
| 2011 |              3 |
| 2017 |              3 |
+------+----------------+
2 rows in set (0.00 sec)
```
--------------------------------------------------------------
9.	Display the details of those employees who earn greater than average of their department. 

```plain
SELECT e_name, salary, average, Employee.dept_no FROM Employee, 
(SELECT dept_no, avg(salary) as average FROM Employee
GROUP BY dept_no) dept_avg_sal
WHERE Employee.dept_no = dept_avg_sal.dept_no
AND salary > average;
```

```plain
mysql> SELECT e_name, salary, average, Employee.dept_no FROM Employee,
    -> (SELECT dept_no, avg(salary) as average FROM Employee
    -> GROUP BY dept_no) dept_avg_sal
    -> WHERE Employee.dept_no = dept_avg_sal.dept_no
    -> AND salary > average;
+----------+--------+------------+---------+
| e_name   | salary | average    | dept_no |
+----------+--------+------------+---------+
| Jaisurya | 100000 | 49000.0000 | D001    |
| Vanshika |  63000 | 53500.0000 | D002    |
| Shubham  |  92000 | 59666.6667 | D003    |
| Anmol    |  68000 | 40000.0000 | D004    |
| Nehal    |  11000 |  7500.0000 | D005    |
| Ram      |  78000 | 41500.0000 | D010    |
| Keshav   |  75000 | 60250.0000 | D012    |
| Adersh   |  75000 | 60250.0000 | D012    |
| Yash     |  72000 | 60250.0000 | D012    |
| Vansh    |  39000 | 29000.0000 | D013    |
+----------+--------+------------+---------+
10 rows in set (0.00 sec)
```
--------------------------------------------------------------
10.	List the employees having salary between 10000 and 20000 

```plain
SELECT e_name, salary FROM Employee
WHERE salary BETWEEN 10000 AND 20000;
```

```plain
mysql> SELECT e_name, salary FROM Employee
    -> WHERE salary BETWEEN 10000 AND 20000;
+----------+--------+
| e_name   | salary |
+----------+--------+
| Nayan    |  19000 |
| Nehal    |  11000 |
| Shivansh |  12000 |
| Prapti   |  19000 |
+----------+--------+
4 rows in set (0.00 sec)
```
--------------------------------------------------------------
11.	Display all employees hired during 1983 (or 2011 in this case)

```plain
SELECT e_name, date_format(hiredate, "%Y") as year FROM employee
WHERE hiredate like "2011-__-__";
```

```plain
mysql> SELECT e_name, date_format(hiredate, "%Y") as year FROM employee
    -> WHERE hiredate like "2011-__-__";
+---------+------+
| e_name  | year |
+---------+------+
| Nehal   | 2011 |
| Shubham | 2011 |
| Vansh   | 2011 |
+---------+------+
3 rows in set (0.00 sec)
```
--------------------------------------------------------------
12.	Update the salaries of all employees in marketing department & hike it by 15%. 

```plain
UPDATE Employee
SET salary = salary + (salary * 0.15)
WHERE dept_no = 
(
	SELECT dept_no FROM Department
	WHERE dept_name = "Marketing"
);
```
--------------------------------------------------------------
13.	Get the gross salaries of all the employees. 

```plain
SELECT e_id, e_name, salary FROM Employee;
```

```plain
mysql> SELECT e_id, e_name, salary FROM Employee;
+------+----------+--------+
| e_id | e_name   | salary |
+------+----------+--------+
| E001 | Nayan    |  19000 |
| E002 | Nehal    |  11000 |
| E003 | Komal    |   2000 |
| E004 | Ram      |  78000 |
| E005 | Shaurya  |  45000 |
| E006 | Keshav   |  75000 |
| E007 | Surya    |  54000 |
| E008 | Anmol    |  68000 |
| E009 | Vanshika |  63000 |
| E010 | Shubham  |  92000 |
| E011 | Kunal    |  44000 |
| E012 | Namit    |   5000 |
| E013 | Raghav   |  90000 |
| E014 | Prakash  |  88000 |
| E015 | Partha   |  33000 |
| E016 | Adersh   |  75000 |
| E017 | Pragnya  |   4000 |
| E018 | Jaisurya | 100000 |
| E019 | Shivansh |  12000 |
| E020 | Yash     |  72000 |
| E021 | Prapti   |  19000 |
| E022 | Vansh    |  39000 |
+------+----------+--------+
22 rows in set (0.00 sec)
```
--------------------------------------------------------------
14.	Get the names of employees and their managers name. 

```plain
SELECT e_id, e_name, manager_name FROM Employee,
(
	SELECT e_id as manager_id, e_name as manager_name FROM Employee
	WHERE e_id IN (SELECT mgr_eid FROM Employee GROUP BY mgr_eid)
) managers
WHERE mgr_eid = manager_id;
```

```plain
mysql> SELECT e_id, e_name, manager_name FROM Employee,
    -> (
    ->  SELECT e_id as manager_id, e_name as manager_name FROM Employee
    ->  WHERE e_id IN (SELECT mgr_eid FROM Employee GROUP BY mgr_eid)
    -> ) managers
    -> WHERE mgr_eid = manager_id;
+------+----------+--------------+
| e_id | e_name   | manager_name |
+------+----------+--------------+
| E001 | Nayan    | Keshav       |
| E002 | Nehal    | Shaurya      |
| E003 | Komal    | Shaurya      |
| E004 | Ram      | Surya        |
| E005 | Shaurya  | Komal        |
| E006 | Keshav   | Vanshika     |
| E007 | Surya    | Keshav       |
| E008 | Anmol    | Keshav       |
| E009 | Vanshika | Nehal        |
| E010 | Shubham  | Komal        |
| E011 | Kunal    | Shubham      |
| E012 | Namit    | Nehal        |
| E013 | Raghav   | Shubham      |
| E014 | Prakash  | Komal        |
| E015 | Partha   | Anmol        |
| E016 | Adersh   | Nayan        |
| E017 | Pragnya  | Shubham      |
| E018 | Jaisurya | Vanshika     |
| E019 | Shivansh | Nehal        |
| E020 | Yash     | Keshav       |
| E021 | Prapti   | Shaurya      |
| E022 | Vansh    | Nayan        |
+------+----------+--------------+
22 rows in set (0.00 sec)
```
--------------------------------------------------------------
15.	Display the name, location and department name of all the employees earning more than 1500. 

```plain
SELECT e_name, loc, dept_name FROM Employee, Department
WHERE salary > 1500
AND Employee.dept_no = Department.dept_no;
```

```plain
mysql> SELECT e_name, loc, dept_name FROM Employee, Department
    -> WHERE salary > 1500
    -> AND Employee.dept_no = Department.dept_no;
+----------+------------+------------------+
| e_name   | loc        | dept_name        |
+----------+------------+------------------+
| Nayan    | Trivandrum | Sales            |
| Nehal    | Delhi      | Finance          |
| Komal    | Hyderabad  | Management       |
| Ram      | Chennai    | Production       |
| Shaurya  | Kolkata    | Management       |
| Keshav   | Kolkata    | Sales            |
| Surya    | Delhi      | Human Resources  |
| Anmol    | Hyderabad  | Legal            |
| Vanshika | Hyderabad  | Administration   |
| Shubham  | Kolkata    | Human Resources  |
| Kunal    | Chennai    | Administration   |
| Namit    | Trivandrum | Production       |
| Raghav   | Hyderabad  | Logisitics       |
| Prakash  | Kolkata    | Customer Service |
| Partha   | Trivandrum | Human Resources  |
| Adersh   | Trivandrum | Sales            |
| Pragnya  | Chennai    | Finance          |
| Jaisurya | Noida      | Management       |
| Shivansh | Hyderabad  | Legal            |
| Yash     | Chennai    | Sales            |
| Prapti   | Trivandrum | Systems          |
| Vansh    | Pune       | Systems          |
+----------+------------+------------------+
22 rows in set (0.00 sec)
```
--------------------------------------------------------------
16.	Show all the employees in Dallas (or Chennai in this case). 

```plain
SELECT e_name, loc FROM Employee
WHERE loc = "Chennai";
```

```plain
mysql> SELECT e_name, loc FROM Employee
    -> WHERE loc = "Chennai";
+---------+---------+
| e_name  | loc     |
+---------+---------+
| Ram     | Chennai |
| Kunal   | Chennai |
| Pragnya | Chennai |
| Yash    | Chennai |
+---------+---------+
4 rows in set (0.00 sec)
```
--------------------------------------------------------------
17.	List the employees name, job, salary, grade, and department for employees in the company except clerks (or Salesperson in this case). Sort on employee names. 

```plain
SELECT e_name, job, salary, grade, dept_name FROM Employee, Department
WHERE job <> "Salesperson"
AND Employee.dept_no = Department.dept_no
ORDER BY e_name;
```

```plain
mysql> SELECT e_name, job, salary, grade, dept_name FROM Employee, Department
    -> WHERE job <> "Salesperson"
    -> AND Employee.dept_no = Department.dept_no
    -> ORDER BY e_name;
+----------+---------------------------------+--------+-------+------------------+
| e_name   | job                             | salary | grade | dept_name        |
+----------+---------------------------------+--------+-------+------------------+
| Anmol    | Legal Advisor                   |  68000 | B     | Legal            |
| Jaisurya | CEO                             | 100000 | E     | Management       |
| Komal    | CFO                             |   2000 | D     | Management       |
| Kunal    | Receptionist                    |  44000 | B     | Administration   |
| Namit    | Production Engineer             |   5000 | E     | Production       |
| Nehal    | Finance Manager                 |  11000 | B     | Finance          |
| Partha   | HR Recuiter                     |  33000 | A     | Human Resources  |
| Pragnya  | Finance Manager                 |   4000 | B     | Finance          |
| Prakash  | Customer Service Representative |  88000 | B     | Customer Service |
| Prapti   | System Administrator            |  19000 | C     | Systems          |
| Raghav   | Warehouse Manager               |  90000 | D     | Logisitics       |
| Ram      | Production Supervisor           |  78000 | A     | Production       |
| Shaurya  | CTO                             |  45000 | A     | Management       |
| Shivansh | Legal Advisor                   |  12000 | A     | Legal            |
| Shubham  | HR Recuiter                     |  92000 | B     | Human Resources  |
| Surya    | Recruiter                       |  54000 | D     | Human Resources  |
| Vansh    | System Administrator            |  39000 | B     | Systems          |
| Vanshika | Office Administrator            |  63000 | A     | Administration   |
+----------+---------------------------------+--------+-------+------------------+
18 rows in set (0.00 sec)
```
--------------------------------------------------------------
18.	Find the employees who earn the minimum salary for their job. Sort in descending order of salary. 

```plain
SELECT e_name, salary, min_sal AS "Min. salary for this job", Employee.job FROM Employee,
(SELECT job, min(salary) AS min_sal FROM Employee
GROUP BY job) job_min_sal
WHERE Employee.job = job_min_sal.job
AND salary = min_sal
ORDER BY salary DESC;
```

```plain
mysql> SELECT e_name, salary, min_sal AS "Min. salary for this job", Employee.job 
    -> FROM Employee,
    -> (SELECT job, min(salary) AS min_sal FROM Employee
    -> GROUP BY job) job_min_sal
    -> WHERE Employee.job = job_min_sal.job
    -> AND salary = min_sal
    -> ORDER BY salary DESC;
+----------+--------+--------------------------+---------------------------------+
| e_name   | salary | Min. salary for this job | job                             |
+----------+--------+--------------------------+---------------------------------+
| Jaisurya | 100000 |                   100000 | CEO                             |
| Raghav   |  90000 |                    90000 | Warehouse Manager               |
| Prakash  |  88000 |                    88000 | Customer Service Representative |
| Ram      |  78000 |                    78000 | Production Supervisor           |
| Vanshika |  63000 |                    63000 | Office Administrator            |
| Surya    |  54000 |                    54000 | Recruiter                       |
| Shaurya  |  45000 |                    45000 | CTO                             |
| Kunal    |  44000 |                    44000 | Receptionist                    |
| Partha   |  33000 |                    33000 | HR Recuiter                     |
| Nayan    |  19000 |                    19000 | Salesperson                     |
| Prapti   |  19000 |                    19000 | System Administrator            |
| Shivansh |  12000 |                    12000 | Legal Advisor                   |
| Namit    |   5000 |                     5000 | Production Engineer             |
| Pragnya  |   4000 |                     4000 | Finance Manager                 |
| Komal    |   2000 |                     2000 | CFO                             |
+----------+--------+--------------------------+---------------------------------+
15 rows in set (0.00 sec)
```
--------------------------------------------------------------
19.	Find the most recently hired employees in the department (order by hiredate). 

```plain
SELECT e_name, hiredate, Employee.dept_no FROM Employee,
(SELECT dept_no, max(hiredate) AS max_date FROM Employee GROUP BY dept_no) dept_date
WHERE Employee.dept_no = dept_date.dept_no
AND hiredate = max_date
ORDER BY hiredate DESC;
```

```plain
mysql> SELECT e_name, hiredate, Employee.dept_no FROM Employee,
    -> (SELECT dept_no, max(hiredate) AS max_date 
    -> FROM Employee GROUP BY dept_no) dept_date
    -> WHERE Employee.dept_no = dept_date.dept_no
    -> AND hiredate = max_date
    -> ORDER BY hiredate DESC;
+----------+------------+---------+
| e_name   | hiredate   | dept_no |
+----------+------------+---------+
| Pragnya  | 2020-02-02 | D005    |
| Shivansh | 2019-02-06 | D004    |
| Prakash  | 2018-09-16 | D008    |
| Surya    | 2017-11-12 | D003    |
| Ram      | 2017-05-09 | D010    |
| Vanshika | 2017-04-15 | D002    |
| Komal    | 2016-05-18 | D001    |
| Raghav   | 2012-07-22 | D007    |
| Vansh    | 2011-10-05 | D013    |
| Yash     | 2007-05-24 | D012    |
+----------+------------+---------+
10 rows in set (0.00 sec)
```
--------------------------------------------------------------
20.	Find out the difference between highest and lowest salaries. 

```plain
SELECT min(salary), max(salary), (max(salary) - min(salary)) as difference FROM Employee;
```

```plain
mysql> SELECT min(salary), max(salary), 
(max(salary) - min(salary)) as difference FROM Employee;
+-------------+-------------+------------+
| min(salary) | max(salary) | difference |
+-------------+-------------+------------+
|        2000 |      100000 |      98000 |
+-------------+-------------+------------+
1 row in set (0.00 sec)
```
--------------------------------------------------------------

