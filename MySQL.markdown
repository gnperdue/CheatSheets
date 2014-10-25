
## sources

* `dev.mysql.com`

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
