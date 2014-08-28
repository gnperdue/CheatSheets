
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

