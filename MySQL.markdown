
## sources

* `dev.mysql.com`
* Learning MySQL and MariaDB, O'Reilly

## general remarks

* Commands are not case sensitive.
* Commands may span multiple lines.

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

### quit

    ctrl-D
    quit
    QUIT

### inspect a db on the command line

    mysqlshow --count database_name -p

### dates

    select current_date;

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


