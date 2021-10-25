---
title: Cassandra
---
# Linux Namespaces

docker image pull cassandra
docker run --rm -d --name HelloWorld cassandra
docker exec -it HelloWorld bash

nodetool status

cqlsh  -e "describe keyspaces"

### References:

cqlsh

cqlsh> create keyspace HelloWorldKeyspace with replication = {'class':'SimpleStrategy', 'replication_factor':3};

cqlsh> describe keyspaces

use helloworldkeyspace;

cqlsh:helloworldkeyspace>

Create table TinyUrlMap(tiny_url text PRIMARY KEY, fullurl text);

Insert into TinyUrlMap(tiny_url, fullurl) Values('tinyurl.com/chzunwa5', 'https://github.com/');

SELECT * FROM TinyUrlMap WHERE tiny_url = 'tinyurl.com/chzunwa5';

https://teddyma.gitbooks.io/learncassandra/content/client/which_node_to_connect.html

docker image pull redis
docker run --name my-redis-container -d redis 

redis-cli

127.0.0.1:6379> ping
PONG

SET  'tinyurl.com/chzunwa5' 'https://github.com/'

127.0.0.1:6379> GET 'tinyurl.com/chzunwa5'
"https://github.com/"



Learning the Elastic Stack

FileBeat

/var/lib/docker/ maps to \\wsl$\docker-desktop-data\version-pack-data\community\docker\


docker exec -it elk_logstash_1 bash
docker exec -u root -t -i elk_logstash_1 /bin/bash

systemctl status logstash.service


https://vocon-it.com/2016/11/17/logstash-hello-world/


# Logstash

docker volume create logstash_vol

docker run --rm -it -v logstash_vol:/usr/share/logstash/pipeline/ docker.elastic.co/logstash/logstash:7.15.0

\\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes\logstash_vol\_data


Hello World!
{
      "@version" => "1",
    "@timestamp" => 2021-09-30T16:49:25.879Z,
          "host" => "65ab9bd52f0c",
       "message" => "Hello World!"
}

docker volume create logstore


input {
  file {
	path    => "/logstore/sample.syslog"
    start_position => "beginning"
  }
}

output {
  stdout {    
  }
}

docker run --rm -it -v logstash_vol:/usr/share/logstash/pipeline/ -v logstore:/logstore docker.elastic.co/logstash/logstash:7.15.0





\\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes\

https://www.elastic.co/guide/en/logstash/current/configuration-file-structure.html

docker network create elastic


/var/lib/docker/volumes/todo-db/_data






\\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes\pipeline\_data



\\wsl$\docker-desktop-data\mnt\wsl\docker-desktop-data\data\docker\volumes

\\wsl$\docker-desktop-data\version-pack-data\community\docker\volumes\todo-db




docker pull docker.elastic.co/elasticsearch/elasticsearch:7.14.1
docker run --name es01-test --net elastic -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.14.1

docker pull docker.elastic.co/kibana/kibana:7.14.1
docker run --name kib01-test --net elastic -p 5601:5601 -e "ELASTICSEARCH_HOSTS=http://es01-test:9200" docker.elastic.co/kibana/kibana:7.14.1


docker run --rm -it -v ~/settings/:/usr/share/logstash/config/ docker.elastic.co/logstash/logstash:7.15.0


docker run --rm -it -v ~/settings/logstash.yml:/usr/share/logstash/config/logstash.yml docker.elastic.co/logstash/logstash:7.15.0






