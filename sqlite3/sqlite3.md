# SQLite 
---

### Commands

`.databses` lists the open databases
`.open filename` open a database file *filename*
`.exit` exit the sqlite3 programm
`.tables` lists all the tables from the open databases
`.schema tablename` - lists the command which created the table
e.g.
```sql
sqlite> .tables
User
sqlite> .schema User
CREATE TABLE User (
    user_id SMALLINT UNSIGNED UNIQUE,
    user_name VARCHAR(20),
    first_name VARCHAR(20),
    last_name VARCHAR(20),
    password VARCHAR(20),
    CONSTRAINT pk_user_id PRIMARY KEY(user_id)
);
```
`.read filename` read input from a file

### Insert records

single record:
```sql
INSERT INTO Status(username, online, status) 
VALUES("adrianm", True, "green");
```
multiple records:
```sql
INSERT INTO Status(username, online, status) 
VALUES
("adrianm", True, "green"),
("james", True, "yellow"),
("jammie", False, "red");
```
