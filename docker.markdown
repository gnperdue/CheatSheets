
## Create a machine (VM on Mac), connect Docker to it

    docker-machine create --driver virtualbox dev  # if new
    docker-machine start dev
    eval "$(docker-machine env dev)"
    docker-machine ssh dev                         # ssh into the docker host
    docker-machine stop dev                        # when done

## Look at hosts

    docker-machine ls                              # look at hosts

## Get help

    docker-machine help

## Images

    docker images      # see what is available

## Running containers

    docker ps          # see what is running
    docker ps -a       # see everything, even stopped containers
    docker ps -a -q    # get just the container IDs for all jobs
    docker create      # "stage" a container (then `start` it)
    docker stop        # stop a container
    docker kill        # kill a container
    docker start       # start a container
    docker restart     # restart a container
    docker rm          # remove the container (can't `restart` it then)
    docker rm $(docker ps -a -q)$    # remove all stopped containers

## Connect to a service in a container, e.g. `TensorFlow`

First we map 8888 (Jupyter notebook) on the "inside" to 5000 on the "outside"
and run the image containing TensorFlow:

    docker run -it -v "$PWD":/mnist -p 5000:8888 b.gcr.io/tensorflow/tensorflow:latest-devel

(This also maps the current directory to a mount in the docker container.)
Then, we launch `ipython notebook` inside the image. Next, we get the correct
host IP address with:

    docker-machine ls

This will provide a URL, e.g. `tcp://192.168.XYZ.XYZ:ABCD`. Point a browser to
`192.168.XYZ.XYZ:5000` and we will see the notebook.
