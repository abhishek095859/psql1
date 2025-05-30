# psql1

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
