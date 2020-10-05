ex1:

command: psql -d postgres -U db_user
command: CREATE DATABASE db_1;
output: CREATE DATABASE
command: \c db_1;
output: You are now connected to database "db_1" as user "db_user".
command: CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(30), password VARCHAR(10));
output: CREATE TABLE
command: INSERT INTO users (name, password) VALUES ('alice', '123'), ('bob', '456'), ('charlie', '789');
output: INSERT 0 3
command: SELECT * FROM users;
output:
 id |  name   | password 
----+---------+----------
  1 | alice   | 123
  2 | bob     | 456
  3 | charlie | 789
(3 rows)

ex2:

command: INSERT INTO users (name, password) VALUES ('dan', '101112'), ('eve', '131415'), ('faythe', '161718');
output: INSERT 0 3
command: SELECT * FROM users;
output:
 id |  name   | password 
----+---------+----------
  1 | alice   | 123
  2 | bob     | 456
  3 | charlie | 789
  4 | dan     | 101112
  5 | eve     | 131415
  6 | faythe  | 161718
(6 rows)


ex3: 

command: SELECT * FROM users WHERE length(password) > 3  ;
output :
 id |  name  | password 
----+--------+----------
  4 | dan    | 101112
  5 | eve    | 131415
  6 | faythe | 161718
(3 rows)

ex4:

command: ALTER TABLE users ADD COLUMN bio TEXT DEFAULT 'Hello, world!' ;
output: ALTER TABLE
commande: SELECT * FROM users;
output: 
 id |  name   | password |      bio      
----+---------+----------+---------------
  1 | alice   | 123      | Hello, world!
  2 | bob     | 456      | Hello, world!
  3 | charlie | 789      | Hello, world!
  4 | dan     | 101112   | Hello, world!
  5 | eve     | 131415   | Hello, world!
  6 | faythe  | 161718   | Hello, world!
(6 rows)

ex5:

command: UPDATE users SET bio = 'Hello, i am alice'  WHERE name = 'alice';
output: UPDATE 1
command: UPDATE users SET bio = 'Hello, i am bob'  WHERE name = 'bob';
output: UPDATE 1
command: UPDATE users SET bio = 'Hello, i am charlie'  WHERE name = 'charlie';
output: UPDATE 1
command: UPDATE users SET bio = 'Hello, i am dan'  WHERE name = 'dan';
output: UPDATE 1
command: UPDATE users SET bio = 'Hello, i am eve'  WHERE name = 'eve';
output: UPDATE 1
command: UPDATE users SET bio = 'Hello, i am faythe'  WHERE name = 'faythe';
output: UPDATE 1
command: SELECT * FROM users;
output: 
 id |  name   | password |         bio         
----+---------+----------+---------------------
  1 | alice   | 123      | Hello, i am alice
  2 | bob     | 456      | Hello, i am bob
  3 | charlie | 789      | Hello, i am charlie
  4 | dan     | 101112   | Hello, i am dan
  5 | eve     | 131415   | Hello, i am eve
  6 | faythe  | 161718   | Hello, i am faythe
(6 rows)

ex6: 

command: SELECT * FROM users ORDER BY id DESC LIMIT 2;
output: 
 id |  name  | password |        bio         
----+--------+----------+--------------------
  6 | faythe | 161718   | Hello, i am faythe
  5 | eve    | 131415   | Hello, i am eve
(2 rows)

ex7: 

command: SELECT * FROM users WHERE ((id % 2) = 1); 
output: 
 id |  name   | password |         bio         
----+---------+----------+---------------------
  1 | alice   | 123      | Hello, i am alice
  3 | charlie | 789      | Hello, i am charlie
  5 | eve     | 131415   | Hello, i am eve
(3 rows)

ex8:

command: DELETE FROM users WHERE (id % 2 = 0);
output: DELETE 3
command: SELECT * FROM users;
output: 
 id |  name   | password |         bio         
----+---------+----------+---------------------
  1 | alice   | 123      | Hello, i am alice
  3 | charlie | 789      | Hello, i am charlie
  5 | eve     | 131415   | Hello, i am eve
(3 rows)

ex9: 

command: DROP TABLE users; 
output: DROP TABLE
command:  \c postgres; 
output: You are now connected to database "postgres" as user "db_user".
command: DROP DATABASE db_1;
output: DROP DATABASE
   
