---
title: Dockerfile
---
# Dockerfile

It is text file with set of commands to build an docker image.

### Build an image from a Dockerfile

```
docker build -t <name:tag(optional)> <PATH/URL>
```

### Dockerfile

#### Run Command

```
FROM busybox
RUN touch my_data
```

#### Add local Files

```
FROM busybox
ADD my_data.txt /my_data.txt
```

#### Set Environment variable

```
FROM busybox
ENV MONGO_DB_HOST=awesomeserver.com
```

#### Expose Port  

```
FROM busybox
EXPOSE 8080/tcp
```

#### Set working directory
  
```
FROM busybox
WORKDIR bin
```


#### CMD
  
Defines default command for container.

e.g. busybox dockerfile has following CMD.

```
CMD ["sh"]
```

User can override the default specified in CMD by specifying arguments to docker.

```
docker run busybox date  

Sat Mar 27 14:52:43 UTC 2021
```

#### ENTRYPOINT
  
An ENTRYPOINT also defines command for container.

```
FROM busybox
ENTRYPOINT ["echo", "Hello World!"]
```

```
docker run -it test-docker-file
Hello World!
```

Any command line arguments to docker run <image> will be appended after all elements in an exec form ENTRYPOINT.

```
docker run -it test-docker-file arg1 arg2
Hello World! arg1 arg2
```

## References:

* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
* [docker build](https://docs.docker.com/engine/reference/commandline/build/)