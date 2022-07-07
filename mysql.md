---
plugins:
  - tooltip
intro: >-
  The SQL cheat sheet provides you with the most commonly used SQL statements
  for your reference.
background: bg-blue-400
date: '2020-12-16T18:28:43.000Z'
title: MySQL
tags:
  - RDBMS
  - DB
icon: icon-mysql
categories:
  - Database
---

# mysql

## Getting started

### Connect MySQL

```text
mysql -u <user> -p

mysql [db_name]

mysql -h <host> -P <port> -u <user> -p [db_name]

mysql -h <host> -u <user> -p [db_name]
```

### Commons

#### Database

| - | - |
| :--- | :--- |
| `create database` db `;` | Create database |
| `show databases;` | List databases |
| `use` db`;` | Switch to db |
| `drop database` db`;` | Delete db |

#### Table

| - | - |
| :--- | :--- |
| `show tables;` | List tables for current db |
| `show fields from` t`;` | List fields for a table |
| `desc` t`;` | Show table structure |
| `show create table`t`;` | Show create table sql |
| `truncate table`t`;` | Remove all data in a table |
| `drop table`t`;` | Delete table |

#### Proccess

| - | - |
| :--- | :--- |
| `show processlist;` | List processes |
| `kill` pid`;` | kill process |

#### Other

| - | - |
| :--- | :--- |
| `exit` or `\q` | Exit MySQL session |

### Backups

Create a backup

```sql
mysqldump -u user -p db_name > db.sql
```

Export db without schema

```text
mysqldump -u user -p db_name --no-data=true --add-drop-table=false > db.sql
```

Restore a backup

```text
mysql -u user -p db_name < db.sql
```

## Examples {.cols-3}

### Managing tables

Create a new table with three columns

```sql
CREATE TABLE t (
     id INT PRIMARY KEY,
     name VARCHAR NOT NULL,
     price INT DEFAULT 0
);
```

Delete the table from the database

```sql
DROP TABLE t ;
```

Add a new column to the table

```sql
ALTER TABLE t ADD column;
```

Drop column c from the table

```sql
ALTER TABLE t DROP COLUMN c ;
```

Add a constraint

```sql
ALTER TABLE t ADD constraint;
```

Drop a constraint

```sql
ALTER TABLE t DROP constraint;
```

Rename a table from t1 to t2

```sql
ALTER TABLE t1 RENAME TO t2;
```

Rename column c1 to c2

```sql
ALTER TABLE t1 RENAME c1 TO c2 ;
```

Remove all data in a table

```sql
TRUNCATE TABLE t;
```

### Querying data from a table

Query data in columns c1, c2 from a table

```sql
SELECT c1, c2 FROM t
```

Query all rows and columns from a table

```sql
SELECT * FROM t
```

Query data and filter rows with a condition

```sql
SELECT c1, c2 FROM t
WHERE condition
```

Query distinct rows from a table

```sql
SELECT DISTINCT c1 FROM t
WHERE condition
```

Sort the result set in ascending or descending order

```sql
SELECT c1, c2 FROM t
ORDER BY c1 ASC [DESC]
```

Skip offset of rows and return the next n rows

```sql
SELECT c1, c2 FROM t
ORDER BY c1 
LIMIT n OFFSET offset
```

Group rows using an aggregate function

```sql
SELECT c1, aggregate(c2)
FROM t
GROUP BY c1
```

Filter groups using HAVING clause

```sql
SELECT c1, aggregate(c2)
FROM t
GROUP BY c1
HAVING condition
```

### Querying from multiple tables

Inner join t1 and t2

```sql
SELECT c1, c2 
FROM t1
INNER JOIN t2 ON condition
```

Left join t1 and t1

```sql
SELECT c1, c2 
FROM t1
LEFT JOIN t2 ON condition
```

Right join t1 and t2

```sql
SELECT c1, c2 
FROM t1
RIGHT JOIN t2 ON condition
```

Perform full outer join

```sql
SELECT c1, c2 
FROM t1
FULL OUTER JOIN t2 ON condition
```

Produce a Cartesian product of rows in tables

```sql
SELECT c1, c2 
FROM t1
CROSS JOIN t2
```

Another way to perform cross join

```sql
SELECT c1, c2 
FROM t1, t2
```

Join t1 to itself using INNER JOIN clause

```sql
SELECT c1, c2
FROM t1 A
INNER JOIN t1 B ON condition
```

Using SQL Operators Combine rows from two queries

```sql
SELECT c1, c2 FROM t1
UNION [ALL]
SELECT c1, c2 FROM t2
```

Return the intersection of two queries

```sql
SELECT c1, c2 FROM t1
INTERSECT
SELECT c1, c2 FROM t2
```

Subtract a result set from another result set

```sql
SELECT c1, c2 FROM t1
MINUS
SELECT c1, c2 FROM t2
```

Query rows using pattern matching %, \_

```sql
SELECT c1, c2 FROM t1
WHERE c1 [NOT] LIKE pattern
```

Query rows in a list

```sql
SELECT c1, c2 FROM t
WHERE c1 [NOT] IN value_list
```

Query rows between two values

```sql
SELECT c1, c2 FROM t
WHERE  c1 BETWEEN low AND high
```

Check if values in a table is NULL or not

```sql
SELECT c1, c2 FROM t
WHERE  c1 IS [NOT] NULL
```

### Using SQL constraints

Set c1 and c2 as a primary key

```sql
CREATE TABLE t(
    c1 INT, c2 INT, c3 VARCHAR,
    PRIMARY KEY (c1,c2)
);
```

Set c2 column as a foreign key

```sql
CREATE TABLE t1(
    c1 INT PRIMARY KEY,  
    c2 INT,
    FOREIGN KEY (c2) REFERENCES t2(c2)
);
```

Make the values in c1 and c2 unique

```sql
CREATE TABLE t(
    c1 INT, c1 INT,
    UNIQUE(c2,c3)
);
```

Ensure c1 &gt; 0 and values in c1 &gt;= c2

```sql
CREATE TABLE t(
  c1 INT, c2 INT,
  CHECK(c1> 0 AND c1 >= c2)
);
```

Set values in c2 column not NULL

```sql
CREATE TABLE t(
     c1 INT PRIMARY KEY,
     c2 VARCHAR NOT NULL
);
```

### Modifying Data

Insert one row into a table

```sql
INSERT INTO t(column_list)
VALUES(value_list);
```

Insert multiple rows into a table

```sql
INSERT INTO t(column_list)
VALUES (value_list), 
       (value_list), …;
```

Insert rows from t2 into t1

```sql
INSERT INTO t1(column_list)
SELECT column_list
FROM t2;
```

Update new value in the column c1 for all rows

```sql
UPDATE t
SET c1 = new_value;
```

Update values in the column c1, c2 that match the condition

```sql
UPDATE t
SET c1 = new_value, 
        c2 = new_value
WHERE condition;
```

Delete all data in a table

```sql
DELETE FROM t;
```

Delete subset of rows in a table

```sql
DELETE FROM t
WHERE condition;
```

### Managing Views

Create a new view that consists of c1 and c2

```sql
CREATE VIEW v(c1,c2) 
AS
SELECT c1, c2
FROM t;
```

Create a new view with check option

```sql
CREATE VIEW v(c1,c2) 
AS
SELECT c1, c2
FROM t;
WITH [CASCADED | LOCAL] CHECK OPTION;
```

Create a recursive view

```sql
CREATE RECURSIVE VIEW v 
AS
select-statement -- anchor part
UNION [ALL]
select-statement; -- recursive part
```

Create a temporary view

```sql
CREATE TEMPORARY VIEW v 
AS
SELECT c1, c2
FROM t;
```

Delete a view

```sql
DROP VIEW view_name;
```

### Managing triggers

Create or modify a trigger

```sql
CREATE OR MODIFY TRIGGER trigger_name
WHEN EVENT
ON table_name TRIGGER_TYPE
EXECUTE stored_procedure;
```

#### WHEN

| - | - |
| :--- | :--- |
| `BEFORE` | invoke before the event occurs |
| `AFTER` | invoke after the event occurs |

#### EVENT

| - | - |
| :--- | :--- |
| `INSERT` | invoke for INSERT |
| `UPDATE` | invoke for UPDATE |
| `DELETE` | invoke for DELETE |

#### TRIGGER\_TYPE

| - | - |
| :--- | :--- |
| `FOR EACH ROW` |  |
| `FOR EACH STATEMENT` |  |

### Managing indexes

Create an index on c1 and c2 of the t table

```sql
CREATE INDEX idx_name 
ON t(c1,c2);
```

Create a unique index on c3, c4 of the t table

```sql
CREATE UNIQUE INDEX idx_name
ON t(c3,c4)
```

Drop an index

```sql
DROP INDEX idx_name;
```

## Data Types {.cols-3}

### Strings

| - | - |
| :--- | :--- |
| `CHAR` | String \(0 - 255\) |
| `VARCHAR` | String \(0 - 255\) |
| `TINYTEXT` | String \(0 - 255\) |
| `TEXT` | String \(0 - 65535\) |
| `BLOB` | String \(0 - 65535\) |
| `MEDIUMTEXT` | String \(0 - 16777215\) |
| `MEDIUMBLOB` | String \(0 - 16777215\) |
| `LONGTEXT` | String \(0 - 429496­7295\) |
| `LONGBLOB` | String \(0 - 429496­7295\) |
| `ENUM` | One of preset options |
| `SET` | Selection of preset options |

### Date & time

| Data Type | Format |
| :--- | :--- |
| `DATE` | yyyy-MM-dd |
| `TIME` | hh:mm:ss |
| `DATETIME` | yyyy-MM-dd hh:mm:ss |
| `TIMESTAMP` | yyyy-MM-dd hh:mm:ss |
| `YEAR` | yyyy |

### Numeric

| - | - |
| :--- | :--- |
| `TINYINT x` | Integer \(-128 to 127\) |
| `SMALLINT x` | Integer \(-32768 to 32767\) |
| `MEDIUMINT x` | Integer \(-8388608 to 8388607\) |
| `INT x` | Integer \(-2147­483648 to 214748­3647\) |
| `BIGINT x` | Integer \(-9223­372­036­854­775808 to 922337­203­685­477­5807\) |
| `FLOAT` | Decimal \(precise to 23 digits\) |
| `DOUBLE` | Decimal \(24 to 53 digits\) |
| `DECIMAL` | "­DOU­BLE­" stored as string |

## Functions & Operators {.cols-3}

### Strings

* [ASCII\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_ascii){data-tooltip="Return numeric value of left-most character"}
* [BIN\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_bin){data-tooltip="Return a string containing binary representation of a number"}
* [BIT\_LENGTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_bit-length){data-tooltip="Return length of argument in bits"}
* [CHAR\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_char){data-tooltip="Return the character for each integer passed"}
* [CHARACTER\_LENGTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_character-length){data-tooltip="Synonym for CHAR\_LENGTH\(\)"}
* [CHAR\_LENGTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_char-length){data-tooltip="Return number of characters in argument"}
* [CONCAT\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_concat){data-tooltip="Return concatenated string"}
* [CONCAT\_WS\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_concat-ws){data-tooltip="Return concatenate with separator"}
* [ELT\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_elt){data-tooltip="Return string at index number"}
* [EXPORT\_SET\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_export-set){data-tooltip="Return a string such that for every bit set in the value bits, you get an on string and for every unset bit, you get an off string"}
* [FIELD\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_field){data-tooltip="Index \(position\) of first argument in subsequent arguments"}
* [FIND\_IN\_SET\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_find-in-set){data-tooltip="Index \(position\) of first argument within second argument"}
* [FORMAT\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_format){data-tooltip="Return a number formatted to specified number of decimal places"}
* [FROM\_BASE64\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_from-base64){data-tooltip="Decode base64 encoded string and return result"}
* [HEX\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_hex){data-tooltip="Hexadecimal representation of decimal or string value"}
* [INSERT\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_insert){data-tooltip="Insert substring at specified position up to specified number of characters"}
* [INSTR\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_instr){data-tooltip="Return the index of the first occurrence of substring"}
* [LCASE\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_lcase){data-tooltip="Synonym for LOWER\(\)"}
* [LEFT\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_left){data-tooltip="Return the leftmost number of characters as specified"}
* [LENGTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_length){data-tooltip="Return the length of a string in bytes"}
* [LIKE](https://dev.mysql.com/doc/refman/8.0/en/string-comparison-functions.html#operator_like){data-tooltip="Simple pattern matching"}
* [LOAD\_FILE\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_load-file){data-tooltip="Load the named file"}
* [LOCATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_locate){data-tooltip="Return the position of the first occurrence of substring"}
* [LOWER\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_lower){data-tooltip="Return the argument in lowercase"}
* [LPAD\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_lpad){data-tooltip="Return the string argument, left-padded with the specified string"}
* [LTRIM\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_ltrim){data-tooltip="Remove leading spaces"}
* [MAKE\_SET\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_make-set){data-tooltip="Return a set of comma-separated strings that have the corresponding bit in bits set"}
* [MATCH](https://dev.mysql.com/doc/refman/8.0/en/fulltext-search.html#function_match){data-tooltip="Perform full-text search"}
* [MID\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_mid){data-tooltip="Return a substring starting from the specified position"}
* [NOT LIKE](https://dev.mysql.com/doc/refman/8.0/en/string-comparison-functions.html#operator_not-like){data-tooltip="Negation of simple pattern matching"}
* [NOT REGEXP](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#operator_not-regexp){data-tooltip="Negation of REGEXP"}
* [OCT\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_oct){data-tooltip="Return a string containing octal representation of a number"}
* [OCTET\_LENGTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_octet-length){data-tooltip="Synonym for LENGTH\(\)"}
* [ORD\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_ord){data-tooltip="Return character code for leftmost character of the argument"}
* [POSITION\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_position){data-tooltip="Synonym for LOCATE\(\)"}
* [QUOTE\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_quote){data-tooltip="Escape the argument for use in an SQL statement"}
* [REGEXP](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#operator_regexp){data-tooltip="Whether string matches regular expression"}
* [REGEXP\_INSTR\(\)](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#function_regexp-instr){data-tooltip="Starting index of substring matching regular expression"}
* [REGEXP\_LIKE\(\)](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#function_regexp-like){data-tooltip="Whether string matches regular expression"}
* [REGEXP\_REPLACE\(\)](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#function_regexp-replace){data-tooltip="Replace substrings matching regular expression"}
* [REGEXP\_SUBSTR\(\)](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#function_regexp-substr){data-tooltip="Return substring matching regular expression"}
* [REPEAT\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_repeat){data-tooltip="Repeat a string the specified number of times"}
* [REPLACE\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_replace){data-tooltip="Replace occurrences of a specified string"}
* [REVERSE\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_reverse){data-tooltip="Reverse the characters in a string"}
* [RIGHT\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_right){data-tooltip="Return the specified rightmost number of characters"}
* [RLIKE](https://dev.mysql.com/doc/refman/8.0/en/regexp.html#operator_regexp){data-tooltip="Whether string matches regular expression"}
* [RPAD\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_rpad){data-tooltip="Append string the specified number of times"}
* [RTRIM\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_rtrim){data-tooltip="Remove trailing spaces"}
* [SOUNDEX\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_soundex){data-tooltip="Return a soundex string"}
* [SOUNDS LIKE](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#operator_sounds-like){data-tooltip="Compare sounds"}
* [SPACE\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_space){data-tooltip="Return a string of the specified number of spaces"}
* [STRCMP\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-comparison-functions.html#function_strcmp){data-tooltip="Compare two strings"}
* [SUBSTR\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_substr){data-tooltip="Return the substring as specified"}
* [SUBSTRING\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_substring){data-tooltip="Return the substring as specified"}
* [SUBSTRING\_INDEX\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_substring-index){data-tooltip="Return a substring from a string before the specified number of occurrences of the delimiter"}
* [TO\_BASE64\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_to-base64){data-tooltip="Return the argument converted to a base-64 string"}
* [TRIM\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_trim){data-tooltip="Remove leading and trailing spaces"}
* [UCASE\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_ucase){data-tooltip="Synonym for UPPER\(\)"}
* [UNHEX\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_unhex){data-tooltip="Return a string containing hex representation of a number"}
* [UPPER\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_upper){data-tooltip="Convert to uppercase"}
* [WEIGHT\_STRING\(\)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html#function_weight-string){data-tooltip="Return the weight string for a string"}


### Date and Time 

* [ADDDATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_adddate){data-tooltip="Add time values \(intervals\) to a date value"}
* [ADDTIME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_addtime){data-tooltip="Add time"}
* [CONVERT\_TZ\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_convert-tz){data-tooltip="Convert from one time zone to another"}
* [CURDATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_curdate){data-tooltip="Return the current date"}
* [CURRENT\_DATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_current-date){data-tooltip="Synonyms for CURDATE\(\)"}
* [CURRENT\_TIME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_current-time){data-tooltip="Synonyms for CURTIME\(\)"}
* [CURRENT\_TIMESTAMP\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_current-timestamp){data-tooltip="Synonyms for NOW\(\)"}
* [CURTIME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_curtime){data-tooltip="Return the current time"}
* [DATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date){data-tooltip="Extract the date part of a date or datetime expression"}
* [DATE\_ADD\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-add){data-tooltip="Add time values \(intervals\) to a date value"}
* [DATE\_FORMAT\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format){data-tooltip="Format date as specified"}
* [DATE\_SUB\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-sub){data-tooltip="Subtract a time value \(interval\) from a date"}
* [DATEDIFF\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_datediff){data-tooltip="Subtract two dates"}
* [DAY\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_day){data-tooltip="Synonym for DAYOFMONTH\(\)"}
* [DAYNAME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_dayname){data-tooltip="Return the name of the weekday"}
* [DAYOFMONTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_dayofmonth){data-tooltip="Return the day of the month \(0-31\)"}
* [DAYOFWEEK\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_dayofweek){data-tooltip="Return the weekday index of the argument"}
* [DAYOFYEAR\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_dayofyear){data-tooltip="Return the day of the year \(1-366\)"}
* [EXTRACT\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_extract){data-tooltip="Extract part of a date"}
* [FROM\_DAYS\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_from-days){data-tooltip="Convert a day number to a date"}
* [FROM\_UNIXTIME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_from-unixtime){data-tooltip="Format Unix timestamp as a date"}
* [GET\_FORMAT\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_get-format){data-tooltip="Return a date format string"}
* [HOUR\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_hour){data-tooltip="Extract the hour"}
* [LAST\_DAY](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_last-day){data-tooltip="Return the last day of the month for the argument"}
* [LOCALTIME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_localtime){data-tooltip="Synonym for NOW\(\)"}
* [LOCALTIMESTAMP\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_localtimestamp){data-tooltip="Synonym for NOW\(\)"}
* [MAKEDATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_makedate){data-tooltip="Create a date from the year and day of year"}
* [MAKETIME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_maketime){data-tooltip="Create time from hour, minute, second"}
* [MICROSECOND\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_microsecond){data-tooltip="Return the microseconds from argument"}
* [MINUTE\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_minute){data-tooltip="Return the minute from the argument"}
* [MONTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_month){data-tooltip="Return the month from the date passed"}
* [MONTHNAME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_monthname){data-tooltip="Return the name of the month"}
* [NOW\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_now){data-tooltip="Return the current date and time"}
* [PERIOD\_ADD\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_period-add){data-tooltip="Add a period to a year-month"}
* [PERIOD\_DIFF\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_period-diff){data-tooltip="Return the number of months between periods"}
* [QUARTER\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_quarter){data-tooltip="Return the quarter from a date argument"}
* [SEC\_TO\_TIME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_sec-to-time){data-tooltip="Converts seconds to 'hh:mm:ss' format"}
* [SECOND\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_second){data-tooltip="Return the second \(0-59\)"}
* [STR\_TO\_DATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_str-to-date){data-tooltip="Convert a string to a date"}
* [SUBDATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_subdate){data-tooltip="Synonym for DATE\_SUB\(\) when invoked with three arguments"}
* [SUBTIME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_subtime){data-tooltip="Subtract times"}
* [SYSDATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_sysdate){data-tooltip="Return the time at which the function executes"}
* [TIME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_time){data-tooltip="Extract the time portion of the expression passed"}
* [TIME\_FORMAT\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_time-format){data-tooltip="Format as time"}
* [TIME\_TO\_SEC\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_time-to-sec){data-tooltip="Return the argument converted to seconds"}
* [TIMEDIFF\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_timediff){data-tooltip="Subtract time"}
* [TIMESTAMP\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_timestamp){data-tooltip="With a single argument, this function returns the date or datetime expression; with two arguments, the sum of the arguments"}
* [TIMESTAMPADD\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_timestampadd){data-tooltip="Add an interval to a datetime expression"}
* [TIMESTAMPDIFF\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_timestampdiff){data-tooltip="Subtract an interval from a datetime expression"}
* [TO\_DAYS\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_to-days){data-tooltip="Return the date argument converted to days"}
* [TO\_SECONDS\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_to-seconds){data-tooltip="Return the date or datetime argument converted to seconds since Year 0"}
* [UNIX\_TIMESTAMP\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_unix-timestamp){data-tooltip="Return a Unix timestamp"}
* [UTC\_DATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_utc-date){data-tooltip="Return the current UTC date"}
* [UTC\_TIME\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_utc-time){data-tooltip="Return the current UTC time"}
* [UTC\_TIMESTAMP\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_utc-timestamp){data-tooltip="Return the current UTC date and time"}
* [WEEK\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_week){data-tooltip="Return the week number"}
* [WEEKDAY\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_weekday){data-tooltip="Return the weekday index"}
* [WEEKOFYEAR\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_weekofyear){data-tooltip="Return the calendar week of the date \(1-53\)"}
* [YEAR\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_year){data-tooltip="Return the year"}
* [YEARWEEK\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_yearweek){data-tooltip="Return the year and week"}
* [GET\_FORMAT\(\)](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_get-format){data-tooltip="'%m.%d.%Y'"}


### Numeric

* [%, MOD](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_mod){data-tooltip="Modulo operator"}
* [\*](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_times){data-tooltip="Multiplication operator"}
* [+](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_plus){data-tooltip="Addition operator"}
* [-](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_minus){data-tooltip="Minus operator"}
* [-](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_unary-minus){data-tooltip="Change the sign of the argument"}
* [/](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_divide){data-tooltip="Division operator"}
* [ABS\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_abs){data-tooltip="Return the absolute value"}
* [ACOS\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_acos){data-tooltip="Return the arc cosine"}
* [ASIN\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_asin){data-tooltip="Return the arc sine"}
* [ATAN\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_atan){data-tooltip="Return the arc tangent"}
* [ATAN2\(\), ATAN\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_atan2){data-tooltip="Return the arc tangent of the two arguments"}
* [CEIL\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_ceil){data-tooltip="Return the smallest integer value not less than the argument"}
* [CEILING\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_ceiling){data-tooltip="Return the smallest integer value not less than the argument"}
* [CONV\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_conv){data-tooltip="Convert numbers between different number bases"}
* [COS\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_cos){data-tooltip="Return the cosine"}
* [COT\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_cot){data-tooltip="Return the cotangent"}
* [CRC32\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_crc32){data-tooltip="Compute a cyclic redundancy check value"}
* [DEGREES\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_degrees){data-tooltip="Convert radians to degrees"}
* [DIV](https://dev.mysql.com/doc/refman/8.0/en/arithmetic-functions.html#operator_div){data-tooltip="Integer division"}
* [EXP\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_exp){data-tooltip="Raise to the power of"}
* [FLOOR\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_floor){data-tooltip="Return the largest integer value not greater than the argument"}
* [LN\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_ln){data-tooltip="Return the natural logarithm of the argument"}
* [LOG\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_log){data-tooltip="Return the natural logarithm of the first argument"}
* [LOG10\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_log10){data-tooltip="Return the base-10 logarithm of the argument"}
* [LOG2\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_log2){data-tooltip="Return the base-2 logarithm of the argument"}
* [MOD\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_mod){data-tooltip="Return the remainder"}
* [PI\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_pi){data-tooltip="Return the value of pi"}
* [POW\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_pow){data-tooltip="Return the argument raised to the specified power"}
* [POWER\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_power){data-tooltip="Return the argument raised to the specified power"}
* [RADIANS\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_radians){data-tooltip="Return argument converted to radians"}
* [RAND\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_rand){data-tooltip="Return a random floating-point value"}
* [ROUND\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_round){data-tooltip="Round the argument"}
* [SIGN\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_sign){data-tooltip="Return the sign of the argument"}
* [SIN\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_sin){data-tooltip="Return the sine of the argument"}
* [SQRT\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_sqrt){data-tooltip="Return the square root of the argument"}
* [TAN\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_tan){data-tooltip="Return the tangent of the argument"}
* [TRUNCATE\(\)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_truncate){data-tooltip="Truncate to specified number of decimal places"}


### Aggregate

* [AVG\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_avg){data-tooltip="Return the average value of the argument"}
* [BIT\_AND\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_bit-and){data-tooltip="Return bitwise AND"}
* [BIT\_OR\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_bit-or){data-tooltip="Return bitwise OR"}
* [BIT\_XOR\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_bit-xor){data-tooltip="Return bitwise XOR"}
* [COUNT\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_count){data-tooltip="Return a count of the number of rows returned"}
* [COUNT\(DISTINCT\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_count-distinct){data-tooltip="Return the count of a number of different values"}
* [GROUP\_CONCAT\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_group-concat){data-tooltip="Return a concatenated string"}
* [JSON\_ARRAYAGG\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_json-arrayagg){data-tooltip="Return result set as a single JSON array"}
* [JSON\_OBJECTAGG\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_json-objectagg){data-tooltip="Return result set as a single JSON object"}
* [MAX\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_max){data-tooltip="Return the maximum value"}
* [MIN\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_min){data-tooltip="Return the minimum value"}
* [STD\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_std){data-tooltip="Return the population standard deviation"}
* [STDDEV\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_stddev){data-tooltip="Return the population standard deviation"}
* [STDDEV\_POP\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_stddev-pop){data-tooltip="Return the population standard deviation"}
* [STDDEV\_SAMP\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_stddev-samp){data-tooltip="Return the sample standard deviation"}
* [SUM\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_sum){data-tooltip="Return the sum"}
* [VAR\_POP\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_var-pop){data-tooltip="Return the population standard variance"}
* [VAR\_SAMP\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_var-samp){data-tooltip="Return the sample variance"}
* [VARIANCE\(\)](https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html#function_variance){data-tooltip="Return the population standard variance"}


### JSON {.row-span-4}

* [-&gt;](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#operator_json-column-path){data-tooltip="Return value from JSON column after evaluating path; equivalent to JSON\_EXTRACT\(\)."}
* [-&gt;&gt;](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#operator_json-inline-path){data-tooltip="Return value from JSON column after evaluating path and unquoting the result; equivalent to JSON\_UNQUOTE\(JSON\_EXTRACT\(\)\)."}
* [JSON\_ARRAY\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-creation-functions.html#function_json-array){data-tooltip="Create JSON array"}
* [JSON\_ARRAY\_APPEND\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-array-append){data-tooltip="Append data to JSON document"}
* [JSON\_ARRAY\_INSERT\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-array-insert){data-tooltip="Insert into JSON array"}
* [JSON\_CONTAINS\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-contains){data-tooltip="Whether JSON document contains specific object at path"}
* [JSON\_CONTAINS\_PATH\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-contains-path){data-tooltip="Whether JSON document contains any data at path"}
* [JSON\_DEPTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-attribute-functions.html#function_json-depth){data-tooltip="Maximum depth of JSON document"}
* [JSON\_EXTRACT\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-extract){data-tooltip="Return data from JSON document"}
* [JSON\_INSERT\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-insert){data-tooltip="Insert data into JSON document"}
* [JSON\_KEYS\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-keys){data-tooltip="Array of keys from JSON document"}
* [JSON\_LENGTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-attribute-functions.html#function_json-length){data-tooltip="Number of elements in JSON document"}
* [JSON\_MERGE\(\) \(deprecated\)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-merge){data-tooltip="Merge JSON documents, preserving duplicate keys. Deprecated synonym for JSON\_MERGE\_PRESERVE\(\)"}
* [JSON\_MERGE\_PATCH\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-merge-patch){data-tooltip="Merge JSON documents, replacing values of duplicate keys"}
* [JSON\_MERGE\_PRESERVE\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-merge-preserve){data-tooltip="Merge JSON documents, preserving duplicate keys"}
* [JSON\_OBJECT\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-creation-functions.html#function_json-object){data-tooltip="Create JSON object"}
* [JSON\_OVERLAPS\(\) \(introduced 8.0.17\)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-overlaps){data-tooltip="Compares two JSON documents, returns TRUE \(1\) if these have any key-value pairs or array elements in common, otherwise FALSE \(0\)"}
* [JSON\_PRETTY\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-utility-functions.html#function_json-pretty){data-tooltip="Print a JSON document in human-readable format"}
* [JSON\_QUOTE\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-creation-functions.html#function_json-quote){data-tooltip="Quote JSON document"}
* [JSON\_REMOVE\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-remove){data-tooltip="Remove data from JSON document"}
* [JSON\_REPLACE\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-replace){data-tooltip="Replace values in JSON document"}
* [JSON\_SCHEMA\_VALID\(\) \(introduced 8.0.17\)](https://dev.mysql.com/doc/refman/8.0/en/json-validation-functions.html#function_json-schema-valid){data-tooltip="Validate JSON document against JSON schema; returns TRUE/1 if document validates against schema, or FALSE/0 if it does not"}
* [JSON\_SCHEMA\_VALIDATION\_REPORT\(\) \(introduced 8.0.17\)](https://dev.mysql.com/doc/refman/8.0/en/json-validation-functions.html#function_json-schema-validation-report){data-tooltip="Validate JSON document against JSON schema; returns report in JSON format on outcome on validation including success or failure and reasons for failure"}
* [JSON\_SEARCH\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-search){data-tooltip="Path to value within JSON document"}
* [JSON\_SET\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-set){data-tooltip="Insert data into JSON document"}
* [JSON\_STORAGE\_FREE\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-utility-functions.html#function_json-storage-free){data-tooltip="Freed space within binary representation of JSON column value following partial update"}
* [JSON\_STORAGE\_SIZE\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-utility-functions.html#function_json-storage-size){data-tooltip="Space used for storage of binary representation of a JSON document"}
* [JSON\_TABLE\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-table-functions.html#function_json-table){data-tooltip="Return data from a JSON expression as a relational table"}
* [JSON\_TYPE\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-attribute-functions.html#function_json-type){data-tooltip="Type of JSON value"}
* [JSON\_UNQUOTE\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html#function_json-unquote){data-tooltip="Unquote JSON value"}
* [JSON\_VALID\(\)](https://dev.mysql.com/doc/refman/8.0/en/json-attribute-functions.html#function_json-valid){data-tooltip="Whether JSON value is valid"}
* [JSON\_VALUE\(\) \(introduced 8.0.21\)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#function_json-value){data-tooltip="Extract value from JSON document at location pointed to by path provided; return this value as VARCHAR\(512\) or specified type"}
* [MEMBER OF\(\) \(introduced 8.0.17\)](https://dev.mysql.com/doc/refman/8.0/en/json-search-functions.html#operator_member-of){data-tooltip="Returns true \(1\) if first operand matches any element of JSON array passed as second operand, otherwise returns false \(0\)"}

 

### Cast

* [BINARY](https://dev.mysql.com/doc/refman/8.0/en/cast-functions.html#operator_binary){data-tooltip="Cast a string to a binary string"}
* [CAST\(\)](https://dev.mysql.com/doc/refman/8.0/en/cast-functions.html#function_cast){data-tooltip="Cast a value as a certain type"}
* [CONVERT\(\)](https://dev.mysql.com/doc/refman/8.0/en/cast-functions.html#function_convert){data-tooltip="Cast a value as a certain type"}


### Flow Control

* [CASE](https://dev.mysql.com/doc/refman/8.0/en/flow-control-functions.html#operator_case){data-tooltip="Case operator"}
* [IF\(\)](https://dev.mysql.com/doc/refman/8.0/en/flow-control-functions.html#function_if){data-tooltip="If/else construct"}
* [IFNULL\(\)](https://dev.mysql.com/doc/refman/8.0/en/flow-control-functions.html#function_ifnull){data-tooltip="Null if/else construct"}
* [NULLIF\(\)](https://dev.mysql.com/doc/refman/8.0/en/flow-control-functions.html#function_nullif){data-tooltip="Return NULL if expr1 = expr2"}


### Information

* [BENCHMARK\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_benchmark){data-tooltip="Repeatedly execute an expression"}
* [CHARSET\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_charset){data-tooltip="Return the character set of the argument"}
* [COERCIBILITY\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_coercibility){data-tooltip="Return the collation coercibility value of the string argument"}
* [COLLATION\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_collation){data-tooltip="Return the collation of the string argument"}
* [CONNECTION\_ID\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_connection-id){data-tooltip="Return the connection ID \(thread ID\) for the connection"}
* [CURRENT\_ROLE\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_current-role){data-tooltip="Return the current active roles"}
* [CURRENT\_USER\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_current-user){data-tooltip="The authenticated user name and host name"}
* [DATABASE\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_database){data-tooltip="Return the default \(current\) database name"}
* [FOUND\_ROWS\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_found-rows){data-tooltip="For a SELECT with a LIMIT clause, the number of rows that would be returned were there no LIMIT clause"}
* [ICU\_VERSION\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_icu-version){data-tooltip="ICU library version"}
* [LAST\_INSERT\_ID\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_last-insert-id){data-tooltip="Value of the AUTOINCREMENT column for the last INSERT"}
* [ROLES\_GRAPHML\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_roles-graphml){data-tooltip="Return a GraphML document representing memory role subgraphs"}
* [ROW\_COUNT\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_row-count){data-tooltip="The number of rows updated"}
* [SCHEMA\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_schema){data-tooltip="Synonym for DATABASE\(\)"}
* [SESSION\_USER\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_session-user){data-tooltip="Synonym for USER\(\)"}
* [SYSTEM\_USER\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_system-user){data-tooltip="Synonym for USER\(\)"}
* [USER\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_user){data-tooltip="The user name and host name provided by the client"}
* [VERSION\(\)](https://dev.mysql.com/doc/refman/8.0/en/information-functions.html#function_version){data-tooltip="Return a string that indicates the MySQL server version"}


### Encryption and Compression

* [AES\_DECRYPT\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_aes-decrypt){data-tooltip="Decrypt using AES"}
* [AES\_ENCRYPT\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_aes-encrypt){data-tooltip="Encrypt using AES"}
* [COMPRESS\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_compress){data-tooltip="Return result as a binary string"}
* [MD5\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_md5){data-tooltip="Calculate MD5 checksum"}
* [RANDOM\_BYTES\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_random-bytes){data-tooltip="Return a random byte vector"}
* [SHA1\(\), SHA\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_sha1){data-tooltip="Calculate an SHA-1 160-bit checksum"}
* [SHA2\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_sha2){data-tooltip="Calculate an SHA-2 checksum"}
* [STATEMENT\_DIGEST\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_statement-digest){data-tooltip="Compute statement digest hash value"}
* [STATEMENT\_DIGEST\_TEXT\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_statement-digest-text){data-tooltip="Compute normalized statement digest"}
* [UNCOMPRESS\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_uncompress){data-tooltip="Uncompress a string compressed"}
* [UNCOMPRESSED\_LENGTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_uncompressed-length){data-tooltip="Return the length of a string before compression"}
* [VALIDATE\_PASSWORD\_STRENGTH\(\)](https://dev.mysql.com/doc/refman/8.0/en/encryption-functions.html#function_validate-password-strength){data-tooltip="Determine strength of password"}

 

### Locking

* [GET\_LOCK\(\)](https://dev.mysql.com/doc/refman/8.0/en/locking-functions.html#function_get-lock){data-tooltip="Get a named lock"}
* [IS\_FREE\_LOCK\(\)](https://dev.mysql.com/doc/refman/8.0/en/locking-functions.html#function_is-free-lock){data-tooltip="Whether the named lock is free"}
* [IS\_USED\_LOCK\(\)](https://dev.mysql.com/doc/refman/8.0/en/locking-functions.html#function_is-used-lock){data-tooltip="Whether the named lock is in use; return connection identifier if true"}
* [RELEASE\_ALL\_LOCKS\(\)](https://dev.mysql.com/doc/refman/8.0/en/locking-functions.html#function_release-all-locks){data-tooltip="Release all current named locks"}
* [RELEASE\_LOCK\(\)](https://dev.mysql.com/doc/refman/8.0/en/locking-functions.html#function_release-lock){data-tooltip="Release the named lock"}

 

### Bit

* [&](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_bitwise-and){data-tooltip="Bitwise AND"}
* [&gt;&gt;](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_right-shift){data-tooltip="Right shift"}
* [&lt;&lt;](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_left-shift){data-tooltip="Left shift"}
* \(\[[https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html\#operator\_bitwise-xor\){data-tooltip="Bitwise\]\(https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html\#operator\_bitwise-xor%29{data-tooltip="Bitwise](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_bitwise-xor%29{data-tooltip="Bitwise]%28https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_bitwise-xor%29{data-tooltip="Bitwise)\) XOR"}
* [BIT\_COUNT\(\)](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#function_bit-count){data-tooltip="Return the number of bits that are set"}
* [\|](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_bitwise-or){data-tooltip="Bitwise OR"}
* [~](https://dev.mysql.com/doc/refman/8.0/en/bit-functions.html#operator_bitwise-invert){data-tooltip="Bitwise inversion"}


### Miscellaneous

* [ANY\_VALUE\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_any-value){data-tooltip="Suppress ONLY\_FULL\_GROUP\_BY value rejection"}
* [BIN\_TO\_UUID\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_bin-to-uuid){data-tooltip="Convert binary UUID to string"}
* [DEFAULT\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_default){data-tooltip="Return the default value for a table column"}
* [GROUPING\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_grouping){data-tooltip="Distinguish super-aggregate ROLLUP rows from regular rows"}
* [INET\_ATON\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_inet-aton){data-tooltip="Return the numeric value of an IP address"}
* [INET\_NTOA\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_inet-ntoa){data-tooltip="Return the IP address from a numeric value"}
* [INET6\_ATON\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_inet6-aton){data-tooltip="Return the numeric value of an IPv6 address"}
* [INET6\_NTOA\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_inet6-ntoa){data-tooltip="Return the IPv6 address from a numeric value"}
* [IS\_IPV4\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_is-ipv4){data-tooltip="Whether argument is an IPv4 address"}
* [IS\_IPV4\_COMPAT\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_is-ipv4-compat){data-tooltip="Whether argument is an IPv4-compatible address"}
* [IS\_IPV4\_MAPPED\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_is-ipv4-mapped){data-tooltip="Whether argument is an IPv4-mapped address"}
* [IS\_IPV6\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_is-ipv6){data-tooltip="Whether argument is an IPv6 address"}
* [IS\_UUID\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_is-uuid){data-tooltip="Whether argument is a valid UUID"}
* [MASTER\_POS\_WAIT\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_master-pos-wait){data-tooltip="Block until the replica has read and applied all updates up to the specified position"}
* [NAME\_CONST\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_name-const){data-tooltip="Cause the column to have the given name"}
* [SLEEP\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_sleep){data-tooltip="Sleep for a number of seconds"}
* [UUID\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_uuid){data-tooltip="Return a Universal Unique Identifier \(UUID\)"}
* [UUID\_SHORT\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_uuid-short){data-tooltip="Return an integer-valued universal identifier"}
* [UUID\_TO\_BIN\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_uuid-to-bin){data-tooltip="Convert string UUID to binary"}
* [VALUES\(\)](https://dev.mysql.com/doc/refman/8.0/en/miscellaneous-functions.html#function_values){data-tooltip="Define the values to be used during an INSERT"}


## Also see

* [Regex in MySQL](https://github.com/song940/wiki/tree/c9e74bdcff44d911d638a634d32d0d7a2751356e/regex/README.md#regex-in-mysql) _\(quickref.me\)_

