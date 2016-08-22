# Startup

    $ neo4j start      # http://localhost:7474/ - run in the background
    $ neo4j console    # get a console we ctrl-c to quit
    $ neo4j stop       # stop the background process

# Misc

* `:help commands` - what commands are available
* `:help keys` - see keyboard shortcuts for the browser interface
* `:play sysinfo` - monitoring
* `:play start` - get the startup welcome menu
* `:play neo4j-sync` - get their cloud thingy
* `:play write code` - get the example dbs to play with
* `:play movie graph` - get the movie graph guide to play with

# Docs

* http://neo4j.com/docs/developer-manual/current/#driver-manual-index
* http://neo4j.com/docs/

# Delete a db

This is ridiculous, but...

    libexec$ pwd
    /usr/local/Cellar/neo4j/3.0.0/libexec
    libexec$ ls
    LICENSES.txt  bin/          conf/         import/       logs/         run/
    UPGRADE.txt   certificates/ data/         lib/          plugins/
    libexec$ rm -rf data/*

This blows away the user password too.
