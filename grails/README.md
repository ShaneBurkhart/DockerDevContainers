# Grails Docker Development Container

## How to use this container
The container is intended to be developed in.  To do this, run the following command:
```
docker run -it --rm shaneburkhart/dev:grails
```

## Persisting data
By default, you go files won't persist when the container is removed.  To prevent losing your files, you need to
create a data-only container and use the `--volumes-from` option when creating this container.

To do this, first create your data-only container:
```
docker run -d -v /app -v /root/.m2 --name grails_data dockerfile/ubuntu true
```
The volume `/app` is where I keep all of my source files.  The volume `/root/.m2` is where maven keeps all of it's 
downloaded dependencies.  This prevents grails from having to download all of the dependencies every time you start
a new dev container.

The container does nothing but hold the volumes we want to persist.  As long as this container isn't removed, the
volumes will still be there.  We name the container `grails_data` for future reference when linking the volumes.

Next, we need to start our dev container:
```
docker run -it --rm --volumes-from grails_data shaneburkhart/dev:grails
```
In this command, we added the `--volumes-from grails_data`.  This references the previously made data container and
adds those volumes to our new container.

# Exposing ports
For applications such as web servers, it is useful to be able to load your site in the browser.  By default, docker does not expose any ports.  My app runs on port 8080 so I will show how to expose that port to localhost:
```
docker run -it --rm --volumes-from grails_data -p 127.0.0.1:8080:8080 shaneburkhart/dev:grails
```
The `-p` flag tells docker to expose the given port.  In this case, we are exposing `127.0.0.1:8080` to the docker container port `8080`.  If the web server ran on 8080 but we wanted to view it in the browser on port 3000, we can change it to `127.0.0.1:3000:8080`. 