Scalability

https://www.lecloud.net/post/7295452622/scalability-for-dummies-part-1-clones

Horizontal Scaling:

Load Balancer:
Public IP Address
Private IP Address

Disk space to keep all 

Backend servers

Session Data Servers
RAID - Redundant Array of Independent Disks
RAID 0 - Stripping
RAID 1 - Duplicate data

horizontal scaling (13:00 - 21:00)
load balancing & caching (21:00 – 29:00)
shared session state (29:00 – 34:00)
RAID (36:00 – 40:00)
shared storage tech (42:00)
database replication (43:00)
load balancing tech (44:00 – 45:00)
session affinity (46:00 – 51:00)
in-memory caching (59:00 – 1:00)
query cache
memcache - Garbage collection, put expiry on object when it is used
Read heavy, Write Heavy

data replication – active:passive (1:11 - 1:14), active:active (1:16 - 1:21)


partitioning (1:21 – 1:34)
data center redundancy (1:33 – 1:39)
security (1:39 – 1:44)

https://en.wikipedia.org/wiki/RAID

CS75 (Summer 2012) Lecture 9 Scalability Harvard Web Development David Malan
https://www.youtube.com/watch?v=-W9F__D3oY4


CS75 (Summer 2012) Lecture 0 HTTP Harvard Web Development David Malan
https://www.youtube.com/watch?v=8KuO4r5CHjM

* Translate hostname (e.g. www.google.com) to an IP address
* Domain name lookup using DNS Server
* DNS system hierarchy: If ISP DNS server does not have entry, it will go to DNS hierarchy up.
* At top ROOT servers
* IP4 address (0-255).(0-255).(0-255).(0-255) 32 bits
* IP6 address 128 bits

GET / HTTP/1.0

Home Routers:
192.168.x.x
172.16.y.y
Private Class A
10.z.z.z

Private addresses
Within the address space, certain networks are reserved for private networks. Packets from these networks are not routed across the public internet. This provides a way for private networks to use internal IP addresses without interfering with other networks. The private networks are

10.0.0.1 - 10.255.255.255

172.16.0.0 - 172.31.255.255

192.168.0.0 - 192.168.255.255

Special addresses
Certain IPv4 addresses are set aside for specific uses:

127.0.0.0	Loopback address (the host’s own interface)
224.0.0.0	IP Multicast
255.255.255.255	Broadcast (sent to all interfaces on network) 
 
https://en.wikipedia.org/wiki/Classful_network

TCP/IP
Port no
HTTP Port no: 80
SMTP Port no: 25

DNS Server

A Record
CNAME - Canonical name

DOM - Document Object Model

https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction

Ajax - Asynchronous JavaScript and XML
New approach to using a number of existing technologies together, including HTML or XHTML, CSS, JavaScript, DOM, XML, XSLT, and most importantly the XMLHttpRequest object.

https://www.javacodegeeks.com/2012/11/tomcat-clustering-series-part-2-session-affinity-load-balancer.html


Session Replication:

Session Stickiness:

Sticky Session with Traefik in Docker Swarm with multiple containers.

http://littlebigextra.com/how-to-maintain-session-persistence-sticky-session-in-docker-swarm-with-multiple-containers/

https://boxboat.com/2017/08/03/deploy-web-app-docker-swarm-sticky-sessions/

https://docs.microsoft.com/en-us/virtualization/community/team-blog/2017/20170419-use-nginx-to-load-balance-across-your-docker-swarm-cluster

https://www.jeroenreijn.com/2015/09/testing-session-replication-with-docker-compose-redis-spring-session.html

<Manager className="org.apache.catalina.ha.session.DeltaManager"

https://ashishontech.xyz/session-replication-in-tomcat/