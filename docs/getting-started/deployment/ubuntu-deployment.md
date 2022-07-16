---
sidebar_position: 1
title: Ubuntu
---

# Ubuntu Deployment

## Install Script
Deploy Trudesk with a simple one-liner on a fresh install of Ubuntu 20.04 LTS

:::note Recommended Options
For the best Trudesk experience it is **recommended** to select **Yes** to install **ElasticSerach** and  **MongoDB** when running the install script.
:::

```bash
curl -L -s https://storage.trudesk.io/install/ubuntu-1.2.sh
```

Once complete you can access your deployment at **http://{ipaddress}:8118**

### Other Notes
- In a production environment you should serve **Trudesk** over `https`. It is recommended to use an `nginx` reverse proxy with `ssl` in front of Trudesk.
Please read the [Nginx Reverse Proxy](/) documentation for more information.

:::caution Update Credentials before Production
Ubuntu install script is publically avaliable and thus the **username** and **password** used within MongoDB are designed for quick deployment for demo purposes. **Please read [Updating MongoDB Credentials](/)** before utilizing your instance in production.
:::

#### Updating MongoDB Credentials
Updating the Credentials for the **trudesk** user on the MongoDB `trudesk` database requires connecting to a `mongo` shell. Usually performed on the server hosting MongoDB. More information on MongoDB [db.updateUser()](https://docs.mongodb.com/manual/reference/method/db.updateUser/)

**Select the `trudesk` database**
```bash
use trudesk;
```

**Update the `trudesk` user password**
```bash
db.updateUser("trudesk", {pwd: passwordPrompt()});
```

**Update the password stored in `config.json`**
```bash
sudo vi /usr/src/trudesk/config.json
```

**Restart Trudesk**
```bash
sudo pm2 restart trudesk
```

## Manual Install
The following guide will assist in setting up a **Trudesk** instance from scratch. Although it is recommended to use the [Install Script](/), in some cases a manual install is preferred.

### NodeJS Install
The following will install NodeJS version 16 LTS.

```bash
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash && \
sudo apt-get install -y nodejs build-essential
```

### MongoDB Install
The following will install MongoDB version 5.0 and the latest compatiable MongoDB Tools.

**MongoDB Server 5.0**
```bash
sudo apt-get install gnupg && \
sudo wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add - && \
sudo echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list && \
sudo apat-get update && sudo apt-get install -y mongodb-org mongo-org-shell && \
sudo systemctl daemon-reload && sudo systemctl enable mongod && systemctl start mongod
```

**MongoDB Tools**
```bash
sudo wget https://repo.mongodb.org/apt/ubuntu/dists/focal/mongodb-org/5.0/multiverse/binary-amd64/mongodb-org-database-tools-extra_5.0.6_amd64.deb && \
sudo dpkg -i mongodb-org-database-tools-extra_5.0.6_amd64.deb && \
sudo rm -rf mongodb-org-database-tools-extra_5.0.6_amd64.deb
```

#### Configure MongoDB
Create the `trudesk` database and the database user used to authenticate the connection to MongoDB.

Within a `mongo` shell. Select the `trudesk` database.
```bash
use trudesk;
```

Create the trudesk user on the `trudesk` database. These credentials are used during the **Trudesk  Install Wizard** to make the secure connection between **Trudesk** and **MongoDB**
```bash
db.createUser({"user": "trudesk", "pwd": "YOUR_PASSWORD", "roles": ["readWrite", "dbAdmin"]});
```

### ElasticSearch Install
ElasticSearch is optional but highly recommended. Without ElasticSearch Trudesk will not have search capabilities.

**ElasticSearch 8**
```bash
sudo wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add && \
sudo echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-8.x.list && \
sudo apt-get update && sudo apt-get install -y apt-transport-https elasticsearch && \
sudo systemctl enable elasticsearch && \
sudo systemctl start elasticsearch
```

:::caution ElasticSearch Auth & SSL
By default, ElasticSearch 8 has authenication and SSL enabled. Trudesk currently does not support ElastichSearch Auth & SSL. **This is currently in active development.** Workaround is to disable ElasticSearch Auth and SSL and only connections from `localhost` *See Below*
:::

#### Disable ElasticSearch Auth & SSL
The below steps are a temporary workaround to disable ElasticSearch Auth & SSL to support Trudesk connections.

```bash
sudo vi /etc/elasticsearch/elasticsearch.yml
```

Edit the following values within the `elasticsearch.yml` configuration file.

```yml
xpack.security.enabled: false
xpack.security.html.ssl:
  enabled: false
```

Restart the ElasticSearch Service
```bash
sudo systemctl restart elasticsearch
```

### Installing Trudesk

**Install Yarn and Grunt CLI**
```bash
sudo npm install -g yarn grunt-cli
```

**Clone and Build Trudesk**
```bash
sudo git clone https://github.com/polonel/trudesk /etc/trudesk && \
cd trudesk && \
sudo touch /etc/trudesk/logs/output.log && \
sudo yarn && \
sudo yarn build
```

### Handling Trudesk Process
The best way to handle the **Trudesk Process** is to utilize [Process Manager 2](https://pm2.keymetrics.io/). **PM2** is a daemon process manager that will help manage the Trudesk process. Visit PM2 for more information.

**Install PM2**
```bash
sudo npm install pm2 -g
```

**Run Trudesk as a PM2 Process**
```bash
sudo NODE_ENV=production pm2 start /etc/trudesk/app.js --name trudesk -l /etc/trudesk/logs/output.log --merge-logs && \
sudo pm2 save && \
sudo pm2 startup
```


