---
title: Docker Storage Drivers
---

These come into picture when we need to write data to container's writable layer.

## Ephemeral (Transient) volume

By default files created/updated in a container are stored in writable container layer. So these changes are lost once container is deleted.

## Persistent Data

### Volumes

These are created and managed by Docker and isolated from host machine.

There is a default volume located at /var/lib/docker/volumes 

```
docker volume ls
docker volume inspect <volume-name>
```

User can also explicitly create volume. This is stored in a directory on the Docker host.

#### Bind Mounts

This involves mounting a file or directory on the host machine.
There is a risk involved in bind mounts that a container process can modify file system on host machine.

## tmpfs Mounts  

In memory storage. e.g. used for storing secrets.

## References:

* [Docker storage drivers](https://docs.docker.com/storage/storagedriver/select-storage-driver/)