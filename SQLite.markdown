
### make a db from a file

    $ sqlite3 -echo -column -header pizza.db < pizza.sql 

### useful startup commands

    sqlite> .help
    sqlite> .headers on
    sqlite> .mode column
    sqlite> .nullvalue ?
    sqlite> .schema
    sqlite> .quit

Also, .q to quit, .h or .he, etc. for help, etc.

