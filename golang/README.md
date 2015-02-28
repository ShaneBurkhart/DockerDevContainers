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
