
## Create a machine (VM on Mac), connect Docker to it

    docker-machine create --driver virtualbox dev  # if new
    docker-machine start dev
    eval "$(docker-machine env dev)"
    docker-machine stop dev                        # when done

## Look at hosts

    docker-machine ls                              # look at hosts

## Get help

    docker-machine help

