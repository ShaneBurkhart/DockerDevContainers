# Golang Docker Development Container

## How to use this container
The container is intended to be developed in.  To do this, run the following command:
```
docker run -it --rm shaneburkhart/dev:golang
```

## Persisting data
By default, you go files won't persist when the container is removed.  To prevent losing your files, you need to
create a data-only container and use the `--volumes-from` option when creating this container.

To do this, first create your data-only container:
```
docker run -d -v /go --name golang_data dockerfile/ubuntu true
```
The container does nothing but hold the volumes we want to persist.  As long as this container isn't removed, the
volumes will still be there.  We name the container `golang_data` for future reference when linking the volumes.

Next, we need to start our dev container:
```
docker run -it --rm --volumes-from golang_data shaneburkhart/dev:golang
```
In this command, we added the `--volumes-from golang_data`.  This references the previously made data container and
adds those volumes to our new container.

## Exposing ports
For applications such as web servers, it is useful to be able to load your site in the browser.  By default, docker does not expose any ports.  My app runs on port 8080 so I will show how to expose that port to localhost:
```
docker run -it --rm --volumes-from golang_data -p 127.0.0.1:8080:8080 shaneburkhart/dev:golang
```
The `-p` flag tells docker to expose the given port.  In this case, we are exposing `127.0.0.1:8080` to the docker container port `8080`.  If the web server ran on 8080 but we wanted to view it in the browser on port 3000, we can change it to `127.0.0.1:3000:8080`. 

## Using Docker in our dev container
Docker is often needed inside of our dev environment.  To do this, there are two options.  You can do [Docker in Docker](https://github.com/jpetazzo/dind) or the simpler route of mounting the host `docker.sock` file.  I prefer the second one out of pure simplicity:
```
docker run -it --rm --volumes-from golang_data -p 127.0.0.1:8080:8080 -v /run/docker.sock:/run/docker.sock shaneburkhart/dev:golang
```
All docker needs to connect to the host's docker daemon is the unix socket `docker.sock`.  The beauty of this implementation is that you can start containers on the host from inside your development environment.

## Adding SSH keys
