---
title: Docker Security
---

## Default engine security

* Kernel namespaces: 
  
	* Processes in each container are isolated using namespaces, so that they cannot see/ impact processes from other container or from host system.

	* Each container has it's own newtowrk stack.
	
* Control groups: 

	Container resources are limited using Cgroups, so that they cannot accidentally overrun the host resources.

* Docker daemon attack surface:

	Docker daemon requires root privileges, so following details must be considered.

	* Only trusted users should be allowed to control docker daemon.

	* Directory sharing between host and container can alter host filesystem.
	
	* REST API endpoint used by docker cli to communicate with docker daemon was changed to use UNIX socket instead of TCP socket.

### Securing Docker Swarm

Manager mode generates a new root certificate authority (CA) along with key pair. Key pair is used to secure communication with other nodes.

Manager also issue a certificate for a new node joining swarm. By default, each node in the swarm renews its certificate every three months. This can be changed using:

	docker swarm update --cert-expiry <TIME PERIOD>

Following command can be used to generate a new CA certificate and key in case of any compromised manager or CA key.

	docker swarm ca --rotate

### Docker Content Trust

This provides ability to verify integrity and publisher in push and pull images operations.


## References:

* [Docker security](https://docs.docker.com/engine/security/)
* [Manage swarm security with public key infrastructure (PKI)](https://docs.docker.com/engine/swarm/how-swarm-mode-works/pki/)