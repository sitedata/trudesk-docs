---
sidebar_position: 1
slug: /
---

# Introduction
Trudesk is Open Source Help Desk Software. Built with one goal in mind, to keep work loads organized and simple. 

This documentation will assist Trudesk users with installation, configuration, and administration of the **Open Source Community Edition** of Trudesk.

Let's discover **Trudesk in less than 5 minutes**.

<p align="center">
  <img src="https://files.trudesk.io/hero-td-right.png" alt="Trudesk Hero Image" />
</p>

## Features
Trudesk has been active development since 2014. Many community requested features have been implemented. Here are just a few things Trudesk Community Edition has to offer. With many more features already **in-progress**.
- 📝 **Tickets**
  - Real time updates through websockets.
  - Organized through Teams, Groups, and Tags
- 💬 **Messaging**
  - Chat between Agent and Customers/Users.
  - Real time online status of Users
- 📧 **Mail**
  - Notification mail sent automatically
  - Generate tickets through polling an IMAP mailbox.
- 📢 **Annoucements**
  - Site wide announcements
- ⚛️ **Developer Friendy**
  - API access for third party developers to integrate with Trudesk.

## Getting Started

Trudesk is built with [NodeJS](https://nodejs.org), [MongoDB](https://mongodb.com), and [ElasticSearch](https://www.elastic.co/) which allows it to run in any cloud provider stack, VM, Docker, or bare metal.

Get started by **deploying an instance**.

## Deploying Instance
Quickly deploy a new instance with [Ubuntu Server](https://ubuntu.com/download/server)

### What you'll need
- [Ubuntu Server](https://ubuntu.com/download/server) 20.04 LTS
  - If installing MongoDB and ElasticSearch, a minium of **2GB** of memory and **5GB** of storage is required.

### Deploy with Ubuntu Install Script
Deploy Trudesk with a simple one-liner on a fresh install of Ubuntu 20.04 LTS

:::note Recommended Options
It is **recommended** to select **Yes** to install **ElasticSerach** and  **MongoDB** when running the install script.
:::

```bash
curl -L -s https://storage.trudesk.io/install/ubuntu-1.2.sh
```

Once complete you can access your deployment at **http://{ipaddress}:8118**

### Other Notes
- In a production environment you should serve **Trudesk** over `https`. It is recommended to use an `nginx` reverse proxy with `ssl` in front of Trudesk.
Please read the [Nginx Reverse Proxy](http://localhost) documentation for more information.

:::caution Update Credentials before Production
Ubuntu install script is publically avaliable and thus the **username** and **password** used within MongoDB are designed for quick deployment for demo purposes. **Please read [Updating MongoDB Credentials](/)** before utilizing your instance in production.
:::

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

## What's Next
Once you finished the install wizard you'll be prompted to login. From here the first steps to any fresh deployment is to **configure Trudesk** for use.
Here are some recommended topics to get you started.
- Setup your [General](/) configuration.
- Get your [Mailer](/) up and running.
- Learn about [Department, Teams, & Groups](/).
- Customize your [Appearance](/).

## Something Not Right?
If you find issues with the documentation or have suggestions on how to improve the documentation please [file an issue](https://github.com/polonel/trudesk/issues) for us. The Community Edition of Trudesk is maintained by a very small team, so any additional support is welcomed with open arms.
