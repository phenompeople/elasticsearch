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