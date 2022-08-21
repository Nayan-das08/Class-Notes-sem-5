%%[[_Lab Files]]%%
%%#lab/dbms%% 
# Experiment 2
Implementing ***constraints*** on tables in SQL.

## Constraints
- [x] NOT NULL
- [x] UNIQUE
- [ ] PRIMARY KEY
- [ ] FOREIGN KEY
- [x] CHECK
- [x] DEFAULT

## Output
### Creating a table for blood donors 
```plain
mysql> CREATE TABLE blood_donation
    -> (
    ->   s_no         int         PRIMARY KEY,
    ->   first_name   varchar(20) NOT NULL,
    ->   last_name    varchar(20),
    ->   ref_id       int         UNIQUE,
    ->   age          int         NOT NULL
    -> );

mysql> DESC blood_donation;
+------------+-------------+------+-----+---------+-------+
| Field      | Type        | Null | Key | Default | Extra |
+------------+-------------+------+-----+---------+-------+
| s_no       | int         | NO   | PRI | NULL    |       |
| first_name | varchar(20) | NO   |     | NULL    |       |
| last_name  | varchar(20) | YES  |     | NULL    |       |
| ref_id     | int         | YES  | UNI | NULL    |       |
| age        | int         | NO   |     | NULL    |       |
+------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)
```

### `NOT NULL` Constraint
```plain
mysql> INSERT INTO blood_donation VALUES
    -> (2, NULL, NULL, 1002, NULL);
ERROR 1048 (23000): Column 'first_name' cannot be null
```

### `UNIQUE` Constraint
```plain
mysql> INSERT INTO blood_donation VALUES
    -> (2, 'Atif', 'Aslam', 1001, 26);
ERROR 1062 (23000): Duplicate entry '1001' for key 'blood_donation.ref_id'
```

### `PRIMARY KEY` Constraint
```plain
mysql> INSERT INTO blood_donation VALUES
    -> (1, 'Andrew', NULL, 1003, 29);
ERROR 1062 (23000): Duplicate entry '1' for key 'blood_donation.PRIMARY'
mysql> INSERT INTO blood_donation VALUES
    -> (NULL, 'Andrew', NULL, 1003, 29);
ERROR 1048 (23000): Column 's_no' cannot be null
```

### `FOREIGN KEY` Constraint

### `CHECK` Constraint 
```plain
mysql> ALTER TABLE blood_donation
    -> ADD CONSTRAINT CHECK (age >= 21);

mysql> INSERT INTO blood_donation VALUES
    -> (1, 'Nayan', 'Das', 1001, 20);
ERROR 3819 (HY000): Check constraint 'blood_donation_chk_1' is violated.
```

### `DEFAULT` age = 21
```plain
mysql> ALTER TABLE blood_donation
    -> ALTER age SET DEFAULT 21;
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESC blood_donation;
+------------+-------------+------+-----+---------+-------+
| Field      | Type        | Null | Key | Default | Extra |
+------------+-------------+------+-----+---------+-------+
| s_no       | int         | NO   | PRI | NULL    |       |
| first_name | varchar(20) | NO   |     | NULL    |       |
| last_name  | varchar(20) | YES  |     | NULL    |       |
| ref_id     | int         | YES  | UNI | NULL    |       |
| age        | int         | NO   |     | 21      |       |
+------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> INSERT INTO blood_donation (s_no, first_name, last_name, ref_id) VALUES
    -> (1, 'Raghav', 'Verma', 1001);
Query OK, 1 row affected (0.12 sec)

mysql> SELECT * FROM blood_donation WHERE s_no = 1;
+------+------------+-----------+--------+-----+
| s_no | first_name | last_name | ref_id | age |
+------+------------+-----------+--------+-----+
|    1 | Raghav     | Verma     |   1001 |  21 |
+------+------------+-----------+--------+-----+
1 row in set (0.00 sec)
```

---

