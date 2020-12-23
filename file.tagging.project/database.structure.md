# File Tagging Database Structure

## Database

```sql
CREATE DATABASE IF NOT EXISTS digitalization;
```

<h2 style="color: red" >Tag Cathegory Table</h2>

The table contains tag cathegories such as Name or Finance, Country, City, Year, Date, Time ... 

```sql
CREATE TABLE IF NOT EXISTS cathegory (
    cathegory_id INT AUTO_INCREMENT PRIMARY KEY,
    cathegory_name VARCHAR(30) NOT NULL UNIQUE,
    cathegory_description VARCHAR(256)
);
```
the results 
```
Query OK, 0 rows affected (0.02 sec)

mysql> show tables;
+--------------------------+
| Tables_in_digitalization |
+--------------------------+
| cathegory                |
+--------------------------+
1 row in set (0.00 sec)

mysql> describe cathegory;
+-----------------------+--------------+------+-----+---------+----------------+
| Field                 | Type         | Null | Key | Default | Extra          |
+-----------------------+--------------+------+-----+---------+----------------+
| cathegory_id          | int          | NO   | PRI | NULL    | auto_increment |
| cathegory_name        | varchar(30)  | NO   | UNI | NULL    |                |
| cathegory_description | varchar(256) | YES  |     | NULL    |                |
+-----------------------+--------------+------+-----+---------+----------------+
3 rows in set (0.01 sec)
```

insert some cathegories:

```sql
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Namen", "First and Last Names");
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Finanzen", "Invoices, Acounts extracts, other money related stuff");
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Auto", "Car related documents");
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Vesicherung", "Insurance related documents");
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Haus", "Home related documents");
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Schule", "School related documents");
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Eltern", "Parents/Grandparents related documents");
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Arbeit", "Work related documents");
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Urlaub", "Vacation related documents");
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Misc", "Miscellanous documents");
INSERT INTO cathegory (cathegory_name, cathegory_description)  
        VALUES  ("Jahre", "Years");
```

result:


```
mysql> SELECT * FROM cathegory;
+--------------+----------------+-------------------------------------------------------+
| cathegory_id | cathegory_name | cathegory_description                                 |
+--------------+----------------+-------------------------------------------------------+
|            1 | Namen          | First and Last Names                                  |
|            2 | Finanzen       | Invoices, Acounts extracts, other money related stuff |
|            3 | Auto           | Car related documents                                 |
|            4 | Vesicherung    | Insurance related documents                           |
|            5 | Haus           | Home related documents                                |
|            6 | Schule         | School related documents                              |
|            7 | Eltern         | Parents/Grandparents related documents                |
|            8 | Arbeit         | Work related documents                                |
|            9 | Urlaub         | Vacation related documents                            |
|           10 | Misc           | Miscellanous documents                                |
+--------------+----------------+-------------------------------------------------------+
10 rows in set (0.00 sec)
```

<h2 style="color: red" >Tag Table</h2>

This table contains unique tags.

```sql
CREATE TABLE IF NOT EXISTS tags (
    tag_id INT AUTO_INCREMENT PRIMARY KEY,
    tag_name VARCHAR(30) NOT NULL UNIQUE,
    tag_description VARCHAR(100),
    cathegory_id INT NOT NULL, 
    FOREIGN KEY (cathegory_id) REFERENCES cathegory(cathegory_id)
);
```

output

```
mysql> describe tag;
+-----------------+--------------+------+-----+---------+----------------+
| Field           | Type         | Null | Key | Default | Extra          |
+-----------------+--------------+------+-----+---------+----------------+
| tag_id          | int          | NO   | PRI | NULL    | auto_increment |
| tag_name        | varchar(30)  | NO   | UNI | NULL    |                |
| tag_description | varchar(100) | YES  |     | NULL    |                |
| cathegory_id    | int          | NO   | UNI | NULL    |                |
+-----------------+--------------+------+-----+---------+----------------+
4 rows in set (0.00 sec)

```

add some tags to the db:

```sql
-- Insert Tags within Namen Cathegory
SELECT cathegory_id FROM cathegory WHERE cathegory_name = "Namen" INTO @cathegory_id;
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "daniel", "Daniel", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "dani", "Daniel", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "dennis", "Daniel", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "viv", "Viviana", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "vivi", "Viviana", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "viviana", "Viviana", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "cornelia", "Viviana", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "lucian", "Lucian", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "luci", "Lucian", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "hanga", "Hanga", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "cotirlea", "Cotirlea", @cathegory_id );
INSERT INTO tag (tag_name, tag_description, cathegory_id) 
        VALUES ( "vio", "Viorica", @cathegory_id );
INSERT INTO tag (tag_name, tag_description, cathegory_id) 
        VALUES ( "ica", "Viorica", @cathegory_id );
INSERT INTO tag (tag_name, tag_description, cathegory_id) 
        VALUES ( "viorica", "Viorica", @cathegory_id );
INSERT INTO tag (tag_name, tag_description, cathegory_id) 
        VALUES ( "ioan", "Ioan", @cathegory_id );
INSERT INTO tag (tag_name, tag_description, cathegory_id) 
        VALUES ( "nelu", "Ioan", @cathegory_id );
INSERT INTO tag (tag_name, tag_description, cathegory_id) 
        VALUES ( "magda", "Magdalena", @cathegory_id );
INSERT INTO tag (tag_name, tag_description, cathegory_id) 
        VALUES ( "magdalena", "Magdalena", @cathegory_id );
INSERT INTO tag (tag_name, tag_description, cathegory_id) 
        VALUES ( "Cotarlea", "Cotarlea", @cathegory_id );


-- Insert Tags within Finanzen Cathegory
SELECT cathegory_id FROM cathegory WHERE cathegory_name = "Finanzen" INTO @cathegory_id;
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "rechnung", "Invoice", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "quittung", "Invoice", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "steuer", "Taxes", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "steuererklärung ", "Taxes declaration", @cathegory_id );


-- Insert Tags within Auto Cathegory
SELECT cathegory_id FROM cathegory WHERE cathegory_name = "Auto" INTO @cathegory_id;
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "auto", "Auto", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "kenzeichen", "Registration Number", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "m-hc-1991", "Registration Number", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)  
       VALUES ( "mhc1991", "Registration Number", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)
       VALUES ( "m hc 1991", "Registration Number", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)
       VALUES ( "bmw", "Car Type", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)
       VALUES ( "320", "Car Type", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)
       VALUES ( "3er", "Car Type", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)
       VALUES ( "kfz", "Car Type", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)
       VALUES ( "kraftfahrzeug", "Car Type", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id)
       VALUES ( "pkw", "Car Type", @cathegory_id );


-- Insert Tags within Vesicherung Cathegory
SELECT cathegory_id FROM cathegory WHERE cathegory_name = "Vesicherung" INTO @cathegory_id;
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "vesicherung", "Vesicherung", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "allianz", "Allianz", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "signal iduna", "Signal Iduna", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "iduna", "Iduna", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "signal", "Signal", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "krankenvesicherung", "Krankenvesicherung", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "haftpflichtversicherung", "Haftpflichtversicherung", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "rechtsschutzversicherung", "Rechtsschutzversicherung", @cathegory_id );


-- Insert Tags within Haus Cathegory
SELECT cathegory_id FROM cathegory WHERE cathegory_name = "Haus" INTO @cathegory_id;
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "haus", "Haus", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "heizung", "Heizung", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "braunaugenstr", "Braunaugenstr. 53", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "53", "Braunaugenstr. 53", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
    VALUES ( "80939", "Postleitzahl", @cathegory_id );


-- Insert Tags within Jahre Cathegory
SELECT cathegory_id FROM cathegory WHERE cathegory_name = "Jahre" INTO @cathegory_id;
INSERT INTO tag (tag_name, tag_description, cathegory_id) 
        VALUES ( "2013", "2013", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
        VALUES ( "2014", "2014", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
        VALUES ( "2015", "2015", @cathegory_id ); 
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
        VALUES ( "2016", "2016", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
        VALUES ( "2017", "2017", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
        VALUES ( "2018", "2018", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
        VALUES ( "2019", "2019", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
        VALUES ( "2020", "2020", @cathegory_id );
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
        VALUES ( "2021", "2021", @cathegory_id );


-- Insert Tags within Eltern Cathegory
SELECT cathegory_id FROM cathegory WHERE cathegory_name = "Eltern" INTO @cathegory_id;
INSERT INTO tags (tag_name, tag_description, cathegory_id) 
        VALUES ( "eltern", "Eltern", @cathegory_id );

```


### File Table

This table contains also unique files.

```sql
CREATE TABLE file (
    file_id INT AUTO_INCREMENT PRIMARY KEY,
    file_name VARCHAR(256) UNIQUE NOT NULL,
    file_description VARCHAR(256)
);
```

### File_Tag Table

The table which makes the connection between files and tags. One file can have multiple tags as well as one tag can be found associated with multiple files.
This would be **Many-to-Many** relationship which is realized using the ```File_Tag``` Table.

```sql
CREATE TABLE file_tag (
    file_id SMALLINT UNSIGNED NOT NULL,
    tag_id SMALLINT UNSIGNED NOT NULL,
    FOREIGN KEY (file_id) REFERENCES file(file_id),
    FOREIGN KEY (tag_id) REFERENCES tag(tag_id),
)
```

