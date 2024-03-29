---
title: Docker Images
---

## Manifest

Manifest is the information about an image (e.g. layers, size, digest etc).

   docker manifest inspect busybox
   
```json
        {
                "Ref": "docker.io/library/busybox:latest@sha256:1ccc0a0ca577e5fb5a0bdf2150a1a9f842f47c8865e861fa0062c5d343eb8cac",
                "Descriptor": {
                        "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
                        "digest": "sha256:1ccc0a0ca577e5fb5a0bdf2150a1a9f842f47c8865e861fa0062c5d343eb8cac",
                        "size": 527,
                        "platform": {
                                "architecture": "amd64",
                                "os": "linux"
                        }
                },
                "SchemaV2Manifest": {
                        "schemaVersion": 2,
                        "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
                        "config": {
                                "mediaType": "application/vnd.docker.container.image.v1+json",
                                "size": 1456,
                                "digest": "sha256:388056c9a6838deea3792e8f00705b35b439cf57b3c9c2634fb4e95cfc896de6"
                        },
                        "layers": [
                                {
                                        "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
                                        "size": 764710,
                                        "digest": "sha256:f531cdc67389c92deac44e019e7a1b6fba90d1aaa58ae3e8192f0e0eed747152"
                                }
                        ]
                }
```

   docker image inspect busybox
   
"Id": "sha256:388056c9a6838deea3792e8f00705b35b439cf57b3c9c2634fb4e95cfc896de6",


## Images and Layers


Each instruction in dockerfile creates a layer. These layers are stacked on top of each other.

Docker history command displays the history of an image.

```
docker history nginx

IMAGE          CREATED        CREATED BY                                      SIZE      COMMENT
b8cf2cbeabb9   28 hours ago   /bin/sh -c #(nop)  CMD ["nginx" "-g" "daemon…   0B
<missing>      28 hours ago   /bin/sh -c #(nop)  STOPSIGNAL SIGQUIT           0B
<missing>      28 hours ago   /bin/sh -c #(nop)  EXPOSE 80                    0B
<missing>      28 hours ago   /bin/sh -c #(nop)  ENTRYPOINT ["/docker-entr…   0B
<missing>      28 hours ago   /bin/sh -c #(nop) COPY file:c7f3907578be6851…   4.62kB
<missing>      28 hours ago   /bin/sh -c #(nop) COPY file:0fd5fca330dcd6a7…   1.04kB
<missing>      28 hours ago   /bin/sh -c #(nop) COPY file:0b866ff3fc1ef5b0…   1.96kB
<missing>      28 hours ago   /bin/sh -c #(nop) COPY file:65504f71f5855ca0…   1.2kB
<missing>      28 hours ago   /bin/sh -c set -x     && addgroup --system -…   63.9MB
<missing>      28 hours ago   /bin/sh -c #(nop)  ENV PKG_RELEASE=1~buster     0B
<missing>      28 hours ago   /bin/sh -c #(nop)  ENV NJS_VERSION=0.5.2        0B
<missing>      28 hours ago   /bin/sh -c #(nop)  ENV NGINX_VERSION=1.19.8     0B
<missing>      28 hours ago   /bin/sh -c #(nop)  LABEL maintainer=NGINX Do…   0B
<missing>      43 hours ago   /bin/sh -c #(nop)  CMD ["bash"]                 0B
<missing>      43 hours ago   /bin/sh -c #(nop) ADD file:b2085f4b0a7cb0e57…   69.2MB
```

Docker pull gets each layer separately and stores in local storage area. So, pulling multiple images using common layers result into avoid same layers multiple times.

### Container Layer

Container contains a new writable layer on top called “container layer”. All the container changes are written to this layer.

When container is deleted, this top layer is deleted. Source image remains unmodified.

### The copy-on-write (CoW) strategy

This means that any file/ directory is accessed from lower layer in image, it is used directly from that layer. First time modification is needed on it, it is copied into required layer and modified. 

## References:

* [docker service](https://docs.docker.com/storage/storagedriver/#images-and-layers)