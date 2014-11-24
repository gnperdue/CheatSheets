
### check environment variable is defined

    # use the string "is not null" operator
    if [ -n $MY_ENV_VAR ]; then
        echo "MY_ENV_VAR is defined as $MY_ENV_VAR"
    else
        echo "MY_ENV_VAR is not defined."
    fi 

### check environment variable is not defined

    # use the string "is null" operator
    if [ -z $MY_ENV_VAR ]; then
        echo "MY_ENV_VAR is not defined."
    else
        echo "MY_ENV_VAR is defined as $MY_ENV_VAR"
    fi 

### check available commands/aliases/etc.

`compgen` is a built-in bash command that can list all the Linux commands
you can run.

* `compgen -b` - show all the Bash builtins
* `compgen -k` - show all the Bash keywords
* `compgen -c` - show all the available commands
* `compegn -a` - show all the aliases
* `compgen -A function` - show all the Bash functions

