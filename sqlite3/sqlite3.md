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

```sql
SELECT EmployeeID, LastName, FirstName, City FROM Employee;

SELECT EmployeeID, LastName, FirstName, City FROM Employee WHERE City  == "Calgary";

SELECT EmployeeID, LastName, FirstName, City 
    FROM Employee 
    WHERE  City  == "Calgary" AND 
           LastName == "Edwards";

SELECT EmployeeID, LastName, FirstName, City 
    FROM Employee 
    ORDER BY LastName;

SELECT COUNT(*) FROM Employee;

SELECT City, COUNT(*)
    FROM Employee 
    GROUP BY City;

SELECT City, COUNT(*) as count
    FROM Employee 
    GROUP BY City
    HAVING count > 1;
```

### Artists and Albums

```sql
SELECT Artist.Name, Album.Title
    FROM Artist
    INNER JOIN Album
    ON Artist.ArtistId = Album.ArtistId
    WHERE Artist.Name = "AC/DC";
    SORT BY Album.Title;

# or

SELECT Artist.Name AS ArtistName , Album.Title as AlbumTitle
    FROM Artist, Album
    WHERE Artist.ArtistId = Album.ArtistId
    AND ArtistName = "AC/DC"
    ORDER BY AlbumTitle;

SELECT Artist.Name, Album.Title, Track.Name
    FROM Artist
    INNER JOIN Album
    ON Artist.ArtistId = Album.ArtistId
    INNER JOIN Track
    ON Album.AlbumId = Track.AlbumId
    WHERE Artist.Name = "AC/DC"
    ORDER BY Album.Title, Track.Milliseconds;

SELECT Artist.Name, Count(Track.TrackId) as NumberOfTracks
    FROM Artist
    INNER JOIN Album
    ON Artist.ArtistId = Album.ArtistId
    INNER JOIN Track
    ON Album.AlbumId = Track.AlbumId
    GROUP BY Artist.Name
    ORDER BY NumberOfTracks DESC
    LIMIT 10;


```




