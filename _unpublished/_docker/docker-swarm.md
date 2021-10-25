---
title: Docker Swarm
---

### Initializing swarm cluster

```
docker swarm init 
```

### Get join token commands

```
docker swarm join-token manager
docker swarm join-token worker
```

### Get only join tokens

```
docker swarm join-token manager -q
docker swarm join-token worker -q
```

### List nodes

```
docker node ls
```

#### Create service 

```
docker service create --name <servicename> <imagename>
```

#### Port Mapping

```
docker service create --name=webservice -p 8080:80 nginx
```

#### Routing Mesh  

Docker swarm uses ingress routing mesh by default. All the nodes participate in the routing mesh. 
With routing mesh published service can be accessed through published ports on each node, even if there’s no task running on the node.

This is useful for development environment with simple configuration. Performance gets impacted as incoming requests may get routed to another node.

```
docker service create --name=webservice -p 8080:80 nginx
```

When port 8080 on any node is accessed in above example, Docker routes request to an active container.

#### Bypass routing Mesh - Host Mode

In host mode, any incoming request is listened by instance of service running on the same node. If there is no task running on a node, the service does not listen on that port.

```
docker service create --name=webservice --publish published=8080,target=80,mode=host nginx
```

#### Change no. of tasks

```
docker service create --name=webservice -p 8080:80 --replicas=4 nginx
```

### List services

```
docker service ls
```

### Scale service

```
docker service scale <servicename>=<REPLICAS>
```

#### List tasks
  
```
docker service ps <servicename>
```

#### Inspect
  
```
docker service inspect --pretty <servicename>
```

## References:

* [docker service](https://docs.docker.com/engine/reference/commandline/service/)
* [Use swarm mode routing mesh](https://docs.docker.com/engine/swarm/ingress/#/publish-a-port-for-a-service)