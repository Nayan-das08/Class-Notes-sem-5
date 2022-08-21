%%[[_Lab Files]]%%
%%#lab/dbms%%
# Experiment 1
Executing the **Data Definition Language** and **Data Manipulation Language** commands.

## Commands
**DDL Commands**
- CREATE
- ALTER
- DROP
- RENAME
- TRUNCATE

**DML Commands**
- SELECT
- INSERT
- UPDATE
- DELETE

## Output
### Create and use the database (DDL: `CREATE`)
```plain
mysql> CREATE DATABASE Lab1_Jul22;
Query OK, 1 row affected (0.13 sec)

mysql> USE lab1_jul22
Database changed
```

### Create a table in the database with given info of attributes (DDL: `CREATE`)
```plain
mysql> CREATE TABLE students
    -> (
    ->   roll_no int,
    ->   name    varchar(20),
    ->   marks   int,
    ->   minor   varchar(50)
    -> );
Query OK, 0 rows affected (0.14 sec)

mysql> DESC students;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| roll_no | int         | YES  |     | NULL    |       |
| name    | varchar(20) | YES  |     | NULL    |       |
| marks   | int         | YES  |     | NULL    |       |
| minor   | varchar(50) | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

### Insert values into the table (DML: `INSERT`)
```plain
mysql> INSERT into students values (1, 'Nayan', 88, 'AIML');
Query OK, 1 row affected (0.04 sec)

mysql> SELECT * FROM students;
+---------+-------+-------+-------+
| roll_no | name  | marks | minor |
+---------+-------+-------+-------+
|       1 | Nayan |    88 | AIML  |
+---------+-------+-------+-------+
1 row in set (0.00 sec)

mysql> INSERT into students values
    -> (2, 'Pragnya', 94, 'NULL'),
    -> (3, 'Adersh', 92, 'DataSci'),
    -> (4, 'Yash', 90, 'DataSci'),
    -> (5, 'Shruti', 90, 'DataSci'),
    -> (6, 'Aditya', 96, 'AIML'),
    -> (7, 'Jaisurya', 91, 'DataSci'),
    -> (8, 'Shubham', 93, 'DataSci'),
    -> (9, 'Shivansh', 96, 'AIML');
Query OK, 8 rows affected (0.03 sec)
```

### Displaying all the contents of the table (DML: `SELECT`)
```plain
mysql> SELECT * from students;
+---------+----------+-------+---------+
| roll_no | name     | marks | minor   |
+---------+----------+-------+---------+
|       1 | Nayan    |    88 | AIML    |
|       2 | Pragnya  |    94 | NULL    |
|       3 | Adersh   |    92 | DataSci |
|       4 | Yash     |    90 | DataSci |
|       5 | Shruti   |    90 | DataSci |
|       6 | Aditya   |    96 | AIML    |
|       7 | Jaisurya |    91 | DataSci |
|       8 | Shubham  |    93 | DataSci |
|       9 | Shivansh |    96 | AIML    |
+---------+----------+-------+---------+
9 rows in set (0.00 sec)
```

### Altering the table schema to modify an attribute (DDL: `ALTER`)
```plain
mysql> ALTER TABLE students
    -> MODIFY roll_no int PRIMARY KEY;
Query OK, 0 rows affected (1.45 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESC students;
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| roll_no | int         | NO   | PRI | NULL    |       |
| name    | varchar(20) | YES  |     | NULL    |       |
| marks   | int         | YES  |     | NULL    |       |
| minor   | varchar(50) | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
4 rows in set (0.81 sec)
```

### Update the value for an attribute (DML: `UPDATE`)
```plain
mysql> UPDATE students
    -> SET marks = 91
    -> WHERE roll_no = 1;
Query OK, 1 row affected (0.20 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

### Display all the information for row where roll_no = 1 (DML: `SELECT`)
```plain
mysql> SELECT * FROM students
    -> WHERE roll_no = 1;
+---------+-------+-------+-------+
| roll_no | name  | marks | minor |
+---------+-------+-------+-------+
|       1 | Nayan |    91 | AIML  |
+---------+-------+-------+-------+
1 row in set (0.02 sec)
```

### Delete certain row from the table on the basis of some condition (DML: `DELETE`)
```plain
mysql> DELETE FROM students
    -> WHERE roll_no = 3;
Query OK, 1 row affected (0.19 sec)

mysql> SELECT * FROM students;
+---------+----------+-------+---------+
| roll_no | name     | marks | minor   |
+---------+----------+-------+---------+
|       1 | Nayan    |    91 | AIML    |
|       2 | Pragnya  |    94 | NULL    |
|       4 | Yash     |    90 | DataSci |
|       5 | Shruti   |    90 | DataSci |
|       6 | Aditya   |    96 | AIML    |
|       7 | Jaisurya |    91 | DataSci |
|       8 | Shubham  |    93 | DataSci |
|       9 | Shivansh |    96 | AIML    |
+---------+----------+-------+---------+
8 rows in set (0.00 sec)
```

### Renaming the table in the database (DDL: `RENAME`)
```plain
mysql> show tables;
+----------------------+
| Tables_in_lab1_jul22 |
+----------------------+
| students             |
+----------------------+
1 row in set (0.98 sec)

mysql> RENAME TABLE students TO student_info;
Query OK, 0 rows affected (2.37 sec)

mysql> SHOW TABLES;
+----------------------+
| Tables_in_lab1_jul22 |
+----------------------+
| student_info         |
+----------------------+
1 row in set (0.00 sec)
```

### Deleting all the data from the table (DDL: `TRUNCATE`)
```plain
mysql> TRUNCATE student_info;
Query OK, 0 rows affected (0.26 sec)

mysql> SELECT * FROM student_info;
Empty set (0.00 sec)
```

### Drop the table from the database (DDL: `DROP`)
```plain
mysql> DROP TABLE student_info;
Query OK, 0 rows affected (0.16 sec)

mysql> SHOW TABLES;
Empty set (0.00 sec)
```

