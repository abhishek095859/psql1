# psql1

C:\Users\Minfy>psql --version
psql (PostgreSQL) 17.5

C:\Users\Minfy>psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# CREATE USER uni_admin WITH PASSWORD '1234567890'
postgres-# CREATE USER uni_admin WITH PASSWORD '1234567890';
ERROR:  syntax error at or near "CREATE"
LINE 2: CREATE USER uni_admin WITH PASSWORD '1234567890';
        ^
postgres=# \q

C:\Users\Minfy>psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# CREATE USER uni_admin WITH PASSWORD '1234567890';
CREATE ROLE
postgres=# CREATE DATABASE uni_db OWNER uni_admin;
CREATE DATABASE
postgres=# GRANT ALL PRIVILEGES ON DATABASE uni_db TO uni_admin;
GRANT
postgres=# //q
postgres-# \q

C:\Users\Minfy>psql -U university_admin -d university_db
Password for user university_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "university_admin"

C:\Users\Minfy>psql -U university_admin -d university_db
Password for user university_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "university_admin"

C:\Users\Minfy> psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# ALTER USER uni_admin WITH PASSWORD '12345';
ALTER ROLE
postgres=# GRANT ALL PRIVILEDGES ON DATABASE uni_db TO uni_admin;
ERROR:  syntax error at or near "PRIVILEDGES"
LINE 1: GRANT ALL PRIVILEDGES ON DATABASE uni_db TO uni_admin;
                  ^
postgres=# GRANT ALL PRIVILEGES ON DATABASE uni_db TO uni_admin;
GRANT
postgres=# /q
postgres-# \q

C:\Users\Minfy>psql -U uni_admin -d uni_db;
Password for user uni_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  database "uni_db;" does not exist

C:\Users\Minfy>psql -U uni_admin -d uni_db
Password for user uni_admin:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

uni_db=> CREATE TABLE students(
uni_db(>
uni_db(>
uni_db(>
uni_db(> \\q
invalid command \
Try \? for help.
uni_db(> \q

C:\Users\Minfy>psql -U uni_admin -d uni_db
Password for user uni_admin:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

uni_db=> CREATE TABLE students(
uni_db(> student_id INTEGER,
uni_db(> first_name VARCHAR(50),
uni_db(> last_name VARCHAR(50),
uni_db(> email VARCHAR(50),
uni_db(> dob DATE);
CREATE TABLE
uni_db=> \\dt
invalid command \
Try \? for help.
uni_db=> \\d
invalid command \
Try \? for help.
uni_db=> \d
           List of relations
 Schema |   Name   | Type  |   Owner
--------+----------+-------+-----------
 public | students | table | uni_admin
(1 row)


uni_db=> \dt
           List of relations
 Schema |   Name   | Type  |   Owner
--------+----------+-------+-----------
 public | students | table | uni_admin
(1 row)


uni_db=> ALTER TABLE students ADD COLUMN enrollment_date DATE
uni_db-> ALTER TABLE students ADD COLUMN enrollment_date DATE;
ERROR:  syntax error at or near "ALTER"
LINE 2: ALTER TABLE students ADD COLUMN enrollment_date DATE;
        ^
uni_db=> ALTER TABLE students ADD COLUMN enrollment_date DATE;
ALTER TABLE
uni_db=> ALTER TABLE students DROP COLUMN enrollment_date DATE;
ERROR:  syntax error at or near "DATE"
LINE 1: ALTER TABLE students DROP COLUMN enrollment_date DATE;
                                                         ^
uni_db=> ALTER TABLE students DROP COLUMN enrollment_date;
ALTER TABLE
uni_db=> ALTER TABLE students ALTER COLUMN email TYPE VARCHAR(150);
ALTER TABLE
uni_db=> ALTER TABLE students ADD CONSTRAINT unique_email UNIQUE (email);
ALTER TABLE
uni_db=> ALTER TABLE students ADD COLUMN phone_number TYPE VARCHAR(15);
ERROR:  syntax error at or near "VARCHAR"
LINE 1: ALTER TABLE students ADD COLUMN phone_number TYPE VARCHAR(15...
                                                          ^
uni_db=> ALTER TABLE students ADD COLUMN phone_number VARCHAR(15);
ALTER TABLE
uni_db=> ALTER TABLE students DROP COLUMN phone_number VARCHAR(15);
ERROR:  syntax error at or near "VARCHAR"
LINE 1: ALTER TABLE students DROP COLUMN phone_number VARCHAR(15);
                                                      ^
uni_db=> ALTER TABLE students DROP COLUMN phone_numbER;
ALTER TABLE
uni_db=> ALTER TABLE students DROP COLUMN phone_number;
ERROR:  column "phone_number" of relation "students" does not exist
uni_db=> ALTER TABLE students DROP COLUMN phone_number;
ERROR:  column "phone_number" of relation "students" does not exist
uni_db=> INSERT INTO students(student_id,first_name,last_name,email,dob)
uni_db-> VALUES(1,'Lithin','varma','lithin.varma@gmail.com','2003-09-15');
INSERT 0 1
uni_db=> VALUES(2,'Madhu','kumar','madhu.kumar@gmail.com','2003-07-16');
 column1 | column2 | column3 |        column4        |  column5
---------+---------+---------+-----------------------+------------
       2 | Madhu   | kumar   | madhu.kumar@gmail.com | 2003-07-16
(1 row)


uni_db=> INSERT INTO students(student_id,first_name,last_name,email,dob)
uni_db-> VALUES(3,'john','fancis','john.francis@gmail.com','2003-10-10'),
uni_db-> VALUES(4,'abhi','raj','abhi@gmail.com','2003-11-20'),
uni_db-> VALUES(5,'rahul','kumar','rahul@gmail.com','2003-12-28');
ERROR:  syntax error at or near "VALUES"
LINE 3: VALUES(4,'abhi','raj','abhi@gmail.com','2003-11-20'),
        ^
uni_db=> VALUES(4,'abhi','raj','abhi@gmail.com','2003-11-20');
 column1 | column2 | column3 |    column4     |  column5
---------+---------+---------+----------------+------------
       4 | abhi    | raj     | abhi@gmail.com | 2003-11-20
(1 row)


uni_db=> DELETE FROM students;
DELETE 1
uni_db=> SELECT * FROM students;
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)


uni_db=> INSERT INTO students(student_id,first_name,last_name,email,dob)
uni_db-> VALUES(1,'rahul','chow','rahul.chow@gmail.com','2003-12-10'),
uni_db-> VALUES(2,'Lithin','varma','lithin.varma@gmail.com','2003-09-15'),
uni_db-> VALUES(3,'john','francis','john.francis@gmail.com','2002-12-04'),
uni_db-> VALUES(4,'madhu','kumar','madhu.kumar@gmail.com','2002-06-30'),
uni_db-> VALUES(5,'Jeet','singh','jeet.singh@gmail.com','2003-07-14');
ERROR:  syntax error at or near "VALUES"
LINE 3: VALUES(2,'Lithin','varma','lithin.varma@gmail.com','2003-09-...
        ^
uni_db=> INSERT INTO students(student_id, first_name, last_name, email, dob)
uni_db-> VALUES
uni_db->   (1, 'rahul', 'chow', 'rahul.chow@gmail.com', '2003-12-10'),
uni_db->   (2, 'Lithin', 'varma', 'lithin.varma@gmail.com', '2003-09-15'),
uni_db->   (3, 'john', 'francis', 'john.francis@gmail.com', '2002-12-04'),
uni_db->   (4, 'madhu', 'kumar', 'madhu.kumar@gmail.com', '2002-06-30'),
uni_db->   (5, 'Jeet', 'singh', 'jeet.singh@gmail.com', '2003-07-14');
INSERT 0 5
uni_db=> SELECT * FROM students;
 student_id | first_name | last_name |         email          |    dob
------------+------------+-----------+------------------------+------------
          1 | rahul      | chow      | rahul.chow@gmail.com   | 2003-12-10
          2 | Lithin     | varma     | lithin.varma@gmail.com | 2003-09-15
          3 | john       | francis   | john.francis@gmail.com | 2002-12-04
          4 | madhu      | kumar     | madhu.kumar@gmail.com  | 2002-06-30
          5 | Jeet       | singh     | jeet.singh@gmail.com   | 2003-07-14
(5 rows)


uni_db=> INSERT INTO students(student_id, first_name, last_name, dob)
uni_db-> VALUES(6,'abhi','kumar','2002-02-10');
INSERT 0 1
uni_db=> SELECT * FROM students;
 student_id | first_name | last_name |         email          |    dob
------------+------------+-----------+------------------------+------------
          1 | rahul      | chow      | rahul.chow@gmail.com   | 2003-12-10
          2 | Lithin     | varma     | lithin.varma@gmail.com | 2003-09-15
          3 | john       | francis   | john.francis@gmail.com | 2002-12-04
          4 | madhu      | kumar     | madhu.kumar@gmail.com  | 2002-06-30
          5 | Jeet       | singh     | jeet.singh@gmail.com   | 2003-07-14
          6 | abhi       | kumar     |                        | 2002-02-10
(6 rows)


uni_db=> SELECT * FROM student
uni_db-> WHERE student_id=2;
ERROR:  relation "student" does not exist
LINE 1: SELECT * FROM student
                      ^
uni_db=> SELECT * FROM student,
uni_db-> WHERE student_id=2;
ERROR:  syntax error at or near "WHERE"
LINE 2: WHERE student_id=2;
        ^
uni_db=> SELECT * FROM student WHERE student_id=2;
ERROR:  relation "student" does not exist
LINE 1: SELECT * FROM student WHERE student_id=2;
                      ^
uni_db=> SELECT * FROM students WHERE student_id=2;
 student_id | first_name | last_name |         email          |    dob
------------+------------+-----------+------------------------+------------
          2 | Lithin     | varma     | lithin.varma@gmail.com | 2003-09-15
(1 row)


uni_db=> SELECT * FROM students WHERE dob>'2003-01-01';
 student_id | first_name | last_name |         email          |    dob
------------+------------+-----------+------------------------+------------
          1 | rahul      | chow      | rahul.chow@gmail.com   | 2003-12-10
          2 | Lithin     | varma     | lithin.varma@gmail.com | 2003-09-15
          5 | Jeet       | singh     | jeet.singh@gmail.com   | 2003-07-14
(3 rows)


uni_db=> SELECT * FROM students WHERE dob<'2003-01-01';
 student_id | first_name | last_name |         email          |    dob
------------+------------+-----------+------------------------+------------
          3 | john       | francis   | john.francis@gmail.com | 2002-12-04
          4 | madhu      | kumar     | madhu.kumar@gmail.com  | 2002-06-30
          6 | abhi       | kumar     |                        | 2002-02-10
(3 rows)


uni_db=> SELECT * FROM students WHERE first_name LIKE 'B%' OR first_name LIKE 'C%';
 student_id | first_name | last_name | email | dob
------------+------------+-----------+-------+-----
(0 rows)

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# CREATE USER university_admin WITH PASSWORD 'abhi123';
CREATE ROLE
postgres=# CREATE DATABASE university_db OWNER university_admin;
CREATE DATABASE
postgres=# GRANT ALL PRIVILEGES ON DATABASE university_db TO university_admin;
GRANT
postgres=# \q

C:\Users\Minfy>psql -U university_admin -d university_db
Password for user university_admin:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> CREATE TABLE students (
university_db(> student_id INTEGER,
university_db(> first_name VARCHAR(50),
university_db(> last_name VARCHAR(50)'
university_db'> email VARCHAR(100)'
university_db(> dob DATE);
ERROR:  syntax error at or near "'
email VARCHAR(100)'"
LINE 4: last_name VARCHAR(50)'
                             ^
university_db=>  CREATE TABLE students (
university_db(> university_db(> student_id INTEGER,
university_db(> university_db(> first_name VARCHAR(50),
university_db(> university_db(> last_name VARCHAR(50)'
university_db'> university_db'> email VARCHAR(100)'
university_db'> university_db(> dob DATE);
university_db'>
university_db'>
university_db'>
university_db'> \q

C:\Users\Minfy>psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# CREATE TABLE students (
postgres(#     student_id INTEGER,
postgres(#     first_name VARCHAR(50),
postgres(#     last_name VARCHAR(50),
postgres(#     email VARCHAR(100),
postgres(#     date_of_birth DATE
postgres(# );
CREATE TABLE
postgres=# INSERT INTO students (student_id, first_name, last_name, email, dob)
postgres-# VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
postgres-#        (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...NTO students (student_id, first_name, last_name, email, dob)
                                                                   ^
postgres=# INSERT INTO students (student_id, first_name, last_name, email, dob)
postgres-# VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
postgres-#        (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...NTO students (student_id, first_name, last_name, email, dob)
                                                                   ^
postgres=# INSERT INTO students (student_id, first_name, last_name, email, dob)
postgres-# \q

C:\Users\Minfy>psql -U university_db
Password for user university_db:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "university_db"

C:\Users\Minfy>psql -U university_db
Password for user university_db:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "university_db"

C:\Users\Minfy>psql -U university_admin -d university_db
Password for user university_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: FATAL:  password authentication failed for user "university_admin"

C:\Users\Minfy>psql -U university_admin -d university_db
Password for user university_admin:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> DROP TABLE students
university_db-> DROP TABLE students;
ERROR:  syntax error at or near "DROP"
LINE 2: DROP TABLE students;
        ^
university_db=> DROP TABLE students;
ERROR:  table "students" does not exist
university_db=> CREATE TABLE students (
university_db(>     student_id INTEGER,
university_db(>     first_name VARCHAR(50),
university_db(>     last_name VARCHAR(50),
university_db(>     email VARCHAR(100),
university_db(>     date_of_birth DATE
university_db(> );
CREATE TABLE
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...NTO students (student_id, first_name, last_name, email, dob)
                                                                   ^
university_db=>
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob)
university_db-> VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
university_db->        (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...NTO students (student_id, first_name, last_name, email, dob)
                                                                   ^
university_db=> INSERT INTO students (student_id, first_name, last_name, email, date_of_birth)
university_db-> VALUES (1, 'Alice', 'Smith', 'alice.smith@example.com', '2003-05-15');
INSERT 0 1
university_db=> INSERT INTO students (student_id, first_name, last_name, email, date_of_birth)
university_db-> VALUES (2, 'Bob', 'Johnson', 'bob.johnson@example.com', '2002-08-22'),
university_db-> (3, 'Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10');
INSERT 0 2
university_db=> select * FROM students;
 student_id | first_name | last_name |           email           | date_of_birth
------------+------------+-----------+---------------------------+---------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(3 rows)


university_db=> SELECT * FROM students ORDER BY last_name ASC;
 student_id | first_name | last_name |           email           | date_of_birth
------------+------------+-----------+---------------------------+---------------
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
(3 rows)


university_db=> SELECT * FROM students ORDER BY dob DESC LIMIT 2;
ERROR:  column "dob" does not exist
LINE 1: SELECT * FROM students ORDER BY dob DESC LIMIT 2;
                                        ^
university_db=> SELECT * FROM students ORDER BY date_of_birth DESC LIMIT 2;
 student_id | first_name | last_name |           email           | date_of_birth
------------+------------+-----------+---------------------------+---------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
(2 rows)


university_db=> INSERT INTO students (student_id, first_name, last_name, email, date_of_birth)
university_db-> VALUES (4, 'Abhi', 'Smith', 'abhi.smith@example.com', '2002-10-12');
INSERT 0 1
university_db=> SELECT DISTINCT last_name FROM students;
 last_name
-----------
 Smith
 Johnson
 Brown
(3 rows)


university_db=> SELECT * FROM students;
 student_id | first_name | last_name |           email           | date_of_birth
------------+------------+-----------+---------------------------+---------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Abhi       | Smith     | abhi.smith@example.com    | 2002-10-12
(4 rows)


university_db=> SELECT COUNT(*) FROM students;
 count
-------
     4
(1 row)


university_db=> SELECT COUNT(email) FROM students;
 count
-------
     4
(1 row)


university_db=> SELECT COUNT(DISTINCT) FROM students;
ERROR:  syntax error at or near ")"
LINE 1: SELECT COUNT(DISTINCT) FROM students;
                             ^
university_db=> SELECT DISTINCT COUNT(*) FROM students;
 count
-------
     4
(1 row)


university_db=> SELECT DISTINCT * FROM students;
 student_id | first_name | last_name |           email           | date_of_birth
------------+------------+-----------+---------------------------+---------------
          1 | Alice      | Smith     | alice.smith@example.com   | 2003-05-15
          3 | Charlie    | Brown     | charlie.brown@example.com | 2003-01-10
          4 | Abhi       | Smith     | abhi.smith@example.com    | 2002-10-12
          2 | Bob        | Johnson   | bob.johnson@example.com   | 2002-08-22
(4 rows)


university_db=> SELECT DISTINCT COUNT(last_name) FROM students;
 count
-------
     4
(1 row)


university_db=> SELECT COUNT(DISTINCT last_name) FROM students;
 count
-------
     3
(1 row)


university_db=> SELECT last_name, COUNT(*) AS number_of_students
university_db-> FROM students
university_db-> GROUP BY last_name
university_db->
university_db->
university_db-> ;
 last_name | number_of_students
-----------+--------------------
 Smith     |                  2
 Johnson   |                  1
 Brown     |                  1
(3 rows)


university_db=> SELECT last_name, COUNT(*) AS num_students
university_db-> FROM students
university_db-> GROUP BY last_name
university_db-> ORDER BY num_students FROM DESC;
ERROR:  syntax error at or near "FROM"
LINE 4: ORDER BY num_students FROM DESC;
                              ^
university_db=> SELECT last_name, COUNT(*) AS num_students
university_db-> FROM students
university_db-> GROUP BY last_name
university_db-> ORDER BY num_students DESC;
 last_name | num_students
-----------+--------------
 Smith     |            2
 Johnson   |            1
 Brown     |            1
(3 rows)


university_db=> SELECT last_name, COUNT(*) AS num_students
university_db-> FROM students
university_db-> GROUP BY last_name
university_db-> HAVING COUNT(*)>1
university_db-> ORDER BY num_students DESC;
 last_name | num_students
-----------+--------------
 Smith     |            2
(1 row)


university_db=> SELECT COUNT(DISTINCT first_name) FROM students;
 count
-------
     4
(1 row)


university_db=> DROP TABLE students;
DROP TABLE
university_db=> CREATE TABLE students(
university_db(> student_id INTEGER,
university_db(> first_name VARCHAR(50) NOT NULL,
university_db(> last_name VARCHAR(50) NOT NULL,
university_db(> email VARCHAR(100) UNIQUE,
university_db(> dob DATE,
university_db(> enrollment VARCHAR(10) CHECK(enrollment IN('enrolled','graduated','dropped')));
CREATE TABLE
university_db=> INSERT INTO students (student_id,first_name, last_name, email, dob) VALUES (1, 'Abhi','test', 'test@test.com', '2002-10-12');
INSERT 0 1
university_db=> INSERT INTO students (student_id, last_name, email, dob) VALUES (1,'varma', 'varma@varma.com', '2002-12-27');
ERROR:  null value in column "first_name" of relation "students" violates not-null constraint
DETAIL:  Failing row contains (1, null, varma, varma@varma.com, 2002-12-27, null).
university_db=> INSERT INTO students (student_id, last_name, email, dob) VALUES (1,'varma', 'varma@varma.com', '2002-12-27');
ERROR:  null value in column "first_name" of relation "students" violates not-null constraint
DETAIL:  Failing row contains (1, null, varma, varma@varma.com, 2002-12-27, null).
university_db=> DROP TABLE students;
DROP TABLE
university_db=> CREATE TABLE students (
university_db(> student_id SERIAL PRIMARY KEY,
university_db(> first_name VARCHAR(50) NOT NULL,
university_db(> last VARCHAR(50) NOT NULL,
university_db(> email VARCHAR(100) UNIQUE,
university_db(> dob DATE,
university_db(> enrollment VARCHAR(20) CHECK (enrollment IN ('enrolled','graduated','dropping','pending')));
CREATE TABLE
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
ERROR:  column "last_name" of relation "students" does not exist
LINE 1: INSERT INTO students (first_name, last_name, email, dob, enr...
                                          ^
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
ERROR:  column "last_name" of relation "students" does not exist
LINE 1: INSERT INTO students (first_name, last_name, email, dob, enr...
                                          ^
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
ERROR:  column "last_name" of relation "students" does not exist
LINE 1: INSERT INTO students (first_name, last_name, email, dob, enr...
                                          ^
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
ERROR:  column "last_name" of relation "students" does not exist
LINE 1: INSERT INTO students (first_name, last_name, email, dob, enr...
                                          ^
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Charlie', 'Brown', 'charlie.brown@example.com', '2003-01-10', 'pending');
ERROR:  column "last_name" of relation "students" does not exist
LINE 1: INSERT INTO students (first_name, last_name, email, dob, enr...
                                          ^
university_db=> SELECT * FROM students;
 student_id | first_name | last | email | dob | enrollment
------------+------------+------+-------+-----+------------
(0 rows)


university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment)
university_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
ERROR:  column "last_name" of relation "students" does not exist
LINE 1: INSERT INTO students (first_name, last_name, email, dob, enr...
                                          ^
university_db=> INSERT INTO students (first_name, last, email, dob, enrollment)
university_db-> VALUES ('Alice', 'Smith', 'alice.smith@example.com', '2003-05-15', 'enrolled');
INSERT 0 1
university_db=> INSERT INTO students (first_name, last, email, dob, enrollment)
university_db-> VALUES ('Robert', 'Johnson', 'robert.j@example.com', '2002-08-22', 'enrolled');
INSERT 0 1
university_db=> SELECT * FROM students;
 student_id | first_name |  last   |          email          |    dob     | enrollment
------------+------------+---------+-------------------------+------------+------------
          1 | Alice      | Smith   | alice.smith@example.com | 2003-05-15 | enrolled
          2 | Robert     | Johnson | robert.j@example.com    | 2002-08-22 | enrolled
(2 rows)


university_db=> CREATE TABLE courses (
university_db(> course_id SERIAL PRIMRY KEY,
university_db(> ;
university_db(> );
ERROR:  syntax error at or near "PRIMRY"
LINE 2: course_id SERIAL PRIMRY KEY,
                         ^
university_db=> CREATE TABLE courses (
university_db(> course_id SERIAL PRIMARY KEY,
university_db(> course_name VARCHAR(100) NOT NULL UNIQUE,
university_db(> credits INTEGER CHECK(credits>0 AND credits <10));
CREATE TABLE
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Introduction to SQL', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Database Design', 4);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Web Development', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Data Structures', 4);
INSERT 0 1
university_db=> CREATE TABLE enrollments (
university_db(> enrollment_id SERIAL PRIMARY KEY,
university_db(> student_id INTEGER NOT NULL,
university_db(> course_id INTEGER NOT NULL,
university_db(> enrollment_date DATE DEFAULT CURRENT_DATE,
university_db(> grade CHAR(1) CHECK (grade IN ('A','B','C','D','F','W',NULL)),
university_db(> CONSTRAINT fk_student
university_db(> FOREIGN KEY (student_id)
university_db(> REFERENCES students(student_id)
university_db(> ON DELETE CASCADE,
university_db(> CONSTRAINT fk_course
university_db(> FOREIGN KEY (course_id)
university_db(> REFERENCES courses(course_id)
university_db(> ON DELETE RESTRICT,
university_db(> UNIQUE (student_id,course_id));
CREATE TABLE
university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES (1, 1, 'A');
INSERT 0 1
university_db=> INSERT INTO enrollments (student_id, course_id) VALUES (1, 2);
INSERT 0 1
university_db=>
