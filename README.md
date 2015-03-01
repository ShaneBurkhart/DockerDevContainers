# Docker Development Containers

## Building containers
Each development environment has it's own subdirectory with a Dockerfile. Use the following command to build and push images to docker hub:
```
build-env [ envs... ]
```
By default, this will build each environment and push it to docker hub.  If you don't want to push the image, open the `build-env` script and comment the line `sudo docker push [image]`.

Example use:
```
build-env base java grails
```
The script will build the images in the order specified.

## How to use the environments
To start an environment, run the following:
```
start-env [ env ]
```
This will pull the image from docker hub and start it.  If all goes well, you should be in a new bash shell that is from the image.

To persist data, each environment has a data-only container with a volume for `/home`.  The script checks for a data-only container.  If it exists, the development image uses the volumes from that container.  If it doens't exist, it creates one and uses the volumes from that container.

The containers have also forwarded `docker.sock` from the host so you can use docker in the container.

I imagine your ssh keys won't be in the same place as mine, so to solve that issue, go into the `start-env` script and change the `.ssh` dir to the location of yours on your computer.

Example user:
```
start-env grails
```

Apps and servers are not meant to be run out of these containers.  Instead, these containers are meant to hold your dev tools such as vim and tmux.  To run your apps, you should create a Dockerfile for your app and start that.  You can tell your web container to use volumes from the data-only container used by the dev containers.  This lets you edit code in your dev container and have your app serve that code realtime .
