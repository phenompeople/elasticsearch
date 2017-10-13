[![Docker Automated build](https://img.shields.io/docker/automated/phenompeople/elasticsearch.svg?style=plastic)](https://hub.docker.com/r/phenompeople/elasticsearch/)
[![Docker Build Status](https://img.shields.io/docker/build/phenompeople/elasticsearch.svg?style=plastic)](https://hub.docker.com/r/phenompeople/elasticsearch/)
[![Docker Pulls](https://img.shields.io/docker/pulls/phenompeople/elasticsearch.svg?style=plastic)](https://hub.docker.com/r/phenompeople/elasticsearch/)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

# elasticsearch 

Dockerfiles for building Centos based elasticsearch images.

## Supported tags and respective Dockerfile links

## phenompeople/elasticsearch

* **`latest`		([5.6.2/Dockerfile](https://bitbucket.org/phenompeople/elasticsearch/src/master/5.6.2/Dockerfile))**
* **`5.6.2` 		([5.6.2/Dockerfile](https://bitbucket.org/phenompeople/elasticsearch/src/master/5.6.2/Dockerfile))**
* **`5.5.2` 		([5.5.2/Dockerfile](https://bitbucket.org/phenompeople/elasticsearch/src/master/5.5.2/Dockerfile))**
* **`5.1.2` 		([5.1.2/Dockerfile](https://bitbucket.org/phenompeople/elasticsearch/src/master/5.1.2/Dockerfile))**

### Elasticsearch containers as a cluster without docker-compose 

Since Elasticsearch runs inside a contianer we have to make following changes

1. Docker networking hides the containers from the networking stack on the host machine. The problem is when you start elasticsearch, you have to host addresses. 
   Either we have to publish all ports or update elasticsearch.yml with below settings, and define PUBLISH_IP as an environment variable.
   
   ```
   network.bind_host: 0.0.0.0
   network.publish_host: "${PUBLISH_IP}"
   ```
    
1. Create/update sysctl configurations and Docker startup options to fix max_file_descriptions error during elasticsearch start up.
	/etc/sysconfig/docker with below values
	
	```
	DAEMON_MAXFILES=1048576
	OPTIONS="--default-ulimit nofile=1024:65536"
	DAEMON_PIDFILE_TIMEOUT=10
	```

1. Create/update sysctl.d limits on host machine and update sysctl to reflect immediately

	```
	vm.max_map_count=262144
	fs.file-max=100000
	```
1. Please define below variables during run time to replace default values, variables defined during run time will take the highest priority, each variable should be passed differently with option -e 

|Attribute name                     | Default Value             |
|-----------------------------------|---------------------------|
|ES_JAVA_OPTS                       | -Xms2g -Xmx2g             |

## Pre-Requisites

- install docker-engine [https://docs.docker.com/engine/installation/](https://docs.docker.com/engine/installation/)

## How to use this image 

1.  This image can be used by simply running as a standalone elasticsearch host 

```$ docker run --name=elasticsearch -p 9200:9200 -v /etc/elasticsearch:/usr/local/elasticsearch/config -td phenompeople/elasticsearch```

Above command runs elasticsearch container with port 9200 mapped to host and reading configuration files mapped under /etc/elasticsearch. 

1. In a multi node elasticsearch cluster, to make nodes to communicate each other publish 9300 also in-addition to above command

```$ docker run --name=elasticsearch -p 9200:9200 -p 9300:9300 -v /etc/elasticsearch:/usr/local/elasticsearch/config -td phenompeople/elasticsearch```

1. To make image run even after reboot use extra option --restart=always

```$ docker run --restart=always --name=elasticsearch --name=elasticsearch -p 9200:9200 -p 9300:9300 -v /etc/elasticsearch:/usr/local/elasticsearch/config -td phenompeople/elasticsearch```

## Maintainers

* Rajesh Jonnalagadda (<rajesh.jonnalagadda@phenompeople.com>)

## License and Authors

**License:**	Apache License

**Author :** Phenompeople Pvt Ltd (<admin.squad@phenompeople.com>)