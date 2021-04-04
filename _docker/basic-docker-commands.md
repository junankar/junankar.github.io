---
title: Basic Docker Commands
---
# Basic Docker Commands

## List Images

```
docker images

REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
ubuntu        latest    8e428cff54c8   35 hours ago   72.9MB
hello-world   latest    d1165f221234   3 weeks ago    13.3kB
```
## Docker Run

```
docker run hello-world
```

### Input name

```
docker run --name HelloWorldDocker hello-world
```

###  Interactive Mode  

* --interactive, -i: Keep STDIN open even if not attached
* --tty , -t: Allocate a pseudo-TTY

```
docker run -it ubuntu bash
```

### Automatically delete Docker after user

--rm: Automatically remove the container when it exits
```
docker run --rm -it ubuntu bash
```

### Detached mode

--detach , -d: Run container in background and print container ID
```
docker run -d -it ubuntu bash
docker attach <container>
```

### Port Mapping

```
docker run -d -p 27017:27017 mongo
```

### Use Volumes

```
docker run -ti -v C:\Users\junankar\data:/data ubuntu bash
```


## List Containers

```
docker ps

CONTAINER ID   IMAGE     COMMAND   CREATED         STATUS         PORTS     NAMES
ea6f916df4dc   ubuntu    "bash"    9 seconds ago   Up 8 seconds             pensive_benz
```

## Fetch logs

```
docker logs HelloWorldDocker
```

### List all containers
* --all, -a : Show all containers (default shows just running)
* --latest, -l: Show the latest created container (includes all states)
* --lastm -n: Show n last created containers (includes all states)

ps => "process status"

```
docker ps -a
```

## Create new image

* docker commit - Create a new image from a container’s changes

```
docker commit ea6f916df4dc
sha256:566cef750c7612da5c83a0b761e4227401f3d7b7bdb2302b508698e443a9ec52

```

```
docker commit ea6f916df4dc svendowideit/testimage:version3
```

## Create tag

```
docker tag 566cef750c7612da5c83a0b761e4227401f3d7b7bdb2302b508698e443a9ec52 hello-world-image

```

### References:

* [Docker Reference documentation](https://docs.docker.com/reference/)
