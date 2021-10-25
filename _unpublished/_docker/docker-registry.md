---
title: Docker Registry
---
# Local Registry

```
docker run -d -p 5000:5000 --restart=always -name docker-local-registry registry
```

Pushing image to local registry

```
docker push localhost:5000/my-ubuntu
```

```
docker login localhost:5000
```

```
docker search localhost:5000/library
```

# Docker Trusted Registry


## References:

* [Deploy a registry server](https://docs.docker.com/registry/deploying/)