
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

### quit

    ctrl-D
    quit
    QUIT

