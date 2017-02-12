
## sources

* `dev.mysql.com`
* Learning MySQL and MariaDB, O'Reilly

## general remarks

* Commands are not case sensitive.
* Commands may span multiple lines.
* Use `;` as a command end marker, or `\G` for a different printout (often
with more or more readable detail).

### cancel command entry

    \c

### start/stop the server

    mysql.server start
    mysql.server stop

### log on as root user

    mysql -u root -p

### (over?)empower another user

    grant all privileges on *.* to 'user'@'localhost' identified by 'pass' with grant option;

### log-on/connect as a user

    mysql -h host -u user -p
    mysql -u user -p
    mysql -p
    mysql -p <db_name>

### create a db

    create database database_name;
    use database_name;

### look around

    show databases;
    use my_database;
    show table;
    describe my_table;
    show create table <my_table>\G

### quit

    ctrl-D
    quit
    QUIT

### inspect a db on the command line

    mysqlshow --count database_name -p

### dates

    select current_date;
    SELECT DATE_ADD(CURDATE(), INTERVAL 1 MONTH);

### comparison to `NULL`

    select author, author2 from myLibrary where author2 is NULL;
    select author, author2 from myLibrary where author2 <=> NULL;

### run an SQL file

    source my_sql_file.sql;

### get help

    help;

### set the prompt

    MariaDB [(mydb)]> prompt SQL Command \d>\_
    PROMPT set to 'SQL Command \d>\_'
    SQL Command mydb> prompt SQL>\_
    PROMPT set to 'SQL>\_'
    SQL> prompt db \d>\_
    PROMPT set to 'db \d>\_'
    db mydb>

### back up and restore

    mysqldump --user='user_name' -p mydb my_table > my_table.sql
    mysqldump --user='user_name' -p mydb > mydb.sql
    mysql --user='user_name' -p mydb < mydb.sql  # restore

### wildcards

    SELECT field1, field2
    FROM my_db WHERE field1 LIKE 'A string beginning%';

### study column structure

    SHOW COLUMNS FROM my_table LIKE 'my_column'\G

### column defaults

    ALTER TABLE my_table ALTER my_column SET DEFAULT 7;
    ALTER TABLE my_table ALTER my_column DROP DEFAULT;

### change columns

    ALTER TABLE my_table CHANGE COLUMN col1 col2 INT DEFAULT 3;

### drop a table

    DROP TABLE IF EXISTS my_table;

### enums

    -- add a column to an existing table with enum
    ALTER TABLE my_table
    ADD COLUMN membership_type ENUM('basic', 'premium');

### delete a row

    DELETE FROM my_table WHERE id_number = 101;

### pattern-match to get a list of columns

    SHOW COLUMNS FROM my_table LIKE '%id';

### more info on columns

    SHOW FULL COLUMNS FROM my_table;

### copy a table into a new table in two steps

    CREATE TABLE test.my_table LIKE mydb.my_table;
    INSERT INTO test.my_table SELECT * FROM mydb.my_table;

* Note, to copy into an "existing" table, a good algorithm is to first
back up the table, then drop it, then follow the steps above:

        $ mysqldump --user='user_name' -p mydb mytable > mydb_mytable.sql
        SQL> DROP TABLE mydb.mytable;
        SQL> CREATE TABLE mydb.mytable LIKE test.mytable;
        SQL> INSERT INTO mydb.mytable SELECT * FROM test.mytable;

### ignore dupes and insert the rest

    INSERT IGNORE INTO my_db.my_table
    (field1, field2)
    SELECT field1, field2
    FROM other_db.other_table;

### replace dupes and insert the rest

    REPLACE INTO my_db.my_table
    (field1, field2)
    SELECT field1, field2
    FROM other_db.other_table;

### priorities of inserts

`DELAYED` is deprecated as of MySQL 5.6.6.

    INSERT LOW_PRIORITY INTO ...
    INSERT DELAYED INTO ...
    INSERT HIGH_PRIORITY INTO ...

### multi-table delete examples

    DELETE FROM table1, table2
    USING table1 JOIN table2
    WHERE field1 = 'value'
    AND filed2 LIKE '%another value'
    AND table1.row_id = table2.row_id;

### multi-column update example

    UPDATE my_table
    SET field1 = 'the value',
        a_date = DATE_ADD(CURDATE(), INTERVAL 2 MONTH)
    WHERE row_id = 10;

### delete from multiple tables example

    DELETE FROM table1, table2
    USING table1 JOIN table2
    WHERE table1.field1 = 'a value'
    AND table1.field2 = 'another value'
    AND table1.row_id = table2.the_row_id;

### distinct/unique instances

    SELECT DISTINCT(field1) FROM my_table;

### regexp examples

* `field` contains `value1` or `value2` anywhere

        SELECT field FROM my_table
        WHERE field REGEXP 'value1|value2';

### prevent orphaned rows

    DELETE FROM table1, table2
    USING table1 LEFT JOIN table2
    ON table1.field_id = table2.field_id
    WHERE field1 = 'value'
    AND field2 = 'another value';

### send to upper or lower case

* `LOWER()` or `LCASE()`
* `UPPER()` or `UCASE()`

### 'quote' text

* `QUOTE()`

### trim whitespace

* `LTRIM()`, `RTRIM()`, and `TRIM()`

### padding

* `LPAD()`
* `RPAD()`
* `SPACE()`

### extraction

* `LEFT(<field>, <chars from the left>)`
* `RIGHT(<field>, <chars from the right>)`
* `MID(<field>, <start point>, <# of chars; default=ALL>)`
* `SUBSCTRING()` is the same as `MID()`
* `SUBSTRING(<field FROM <#> FOR <#>)` - wordier syntax
* `SUBSTRING_INDEX(<field>, <separator character>, <# to take>)`

### locating

* `LOCATE()`
* `POSITION(<search string> IN <containing string>)`

### modify strings

* `INSERT()`
* `REPLACE()`

### count rows

    SELECT Count(*) FROM my_table;

### count groups

    SELECT my_field, COUNT(my_field)
    FROM my_table
    GROUP BY my_field;

### get with in a range

`[NOT]` is optiona, of course, depending on intent:

    SELECT my_field FROM my_table
    WHERE [NOT] BETWEEN begin_expr AND end_expr;
