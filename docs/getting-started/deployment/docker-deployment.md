---
sidebar_position: 2
title: Docker
---

# Docker Deployment
Trudesk requires the following addtional docker containers in order to run. Please see the documentation related to those images for additional configuration options you may require.

- [Mongo:5.0](https://hub.docker.com/_/mongo)
- [ElasticSearch:8.0.0](https://hub.docker.com/_/elasticsearch)

## Deploy with Docker-Compose
Within the Github repo, a sample `docker-compose.yml` file is included. We can quickly stand up a demo site with docker. 

**Download `docker-compose.yml` from Github repo**
```bash
wget https://raw.githubusercontent.com/polonel/trudesk/master/docker-compose.yml
```
**Stand Up Docker Stack**
```bash
docker-compose up
```

Three containers are deployed; **MongoDB**, **ElasticSearch**, **Trudesk**. Once all containers are online, access the Trudesk instance at [http://localhost:8118](http://localhost:8118)

*Note: By default MongoDB and Elastic search ports are exposed to the host*

## Manual Deployment
:::note Example Configuration
The following Docker configuration is presented as an example. Your configuration may require addtional options depending on your deployment
:::

### Setup Storage Directories
Create directories to store the data for the containers we are going to deploy. Data directories are needed for **MongDB**, **ElasticSearch**, and **Trudesk**

```bash
sudo mkdir -p /data/db & \
sudo mkdir -p /data/configdb & \
sudo mkdir -p /data/es/data & \
sudo mkdir -p /data/trudesk/plugins & \
sudo mkdir -p /data/trudesk/uploads & \
sudo mkdir -p /data/trudesk/backups & \
```

### MongoDB 5
Run the deployment command to start a **MongoDB 5** container with storage path of `/data/db`. Please refer to the [MongoDB Docker Documentation](https://hub.docker.com/_/mongo) for additional configuration options.

```bash
docker run --name mongodb \
-v /data/db:/data/db \
-v /data/configdb:/data/configdb \
-p 27017:27017 \
-d mongo:5.0
```

### ElasticSearch 8
Run the deployment command to start a **ElasticSearch 8** container with a storage path of `/data/es/data`. Please refer to the [ElasticSearch Docker Documentation](https://hub.docker.com/_/elasticsearch) for additional configuration options.

```bash
docker run --name elasticsearch \
-p 9200:9200 \
-p 9300:9300 \
-v /data/es/data:/usr/share/elasticsearch/data
-e xpack.security.enabled=false \
-e xpack.security.http.ssl.enabled=false \
-e node.name=estrudesk01 \
-e cluster.initial_master_nodes=estrudesk01 \
-e discovery.seed_hosts=estrudesk01 \
-e bootstrap.memory_lock=true
-d elasticsearch:8.0.0
```


### Trudesk
Pull the latest release of Trudesk from Docker.
```bash
sudo docker pull polonel/trudesk:latest
```

```bash
docker run --name trudesk --link mongodb:mongodb \
    -v /data/trudesk/uploads:/usr/src/trudesk/public/uploads \
    -v /data/trudesk/plugins:/usr/src/trudesk/plugins \
    -v /data/trudesk/backups:/usr/src/trudesk/backups \
    -e NODE_ENV=production \
    -e TRUDESK_DOCKER=true \
    -e TD_MONGODB_SERVER=mongodb -e TD_MONGODB_DATABASE=trudesk \
    -e ELATICSEARCH_URI="http://elasticsearch:9200" \
    -p 8118:8118 \
    -d polonel/trudesk:latest
```