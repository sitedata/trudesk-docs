---
sidebar_position: 5
title: Nginx Reverse Proxy
---

# Nginx Reverse Proxy

Trudesk runs on an internal port `8118`. It is recommended to setup a reverse proxy infront of Trudesk to serve `https` connections.
It will also allow you to run multiple instances of trudesk for loadbalancing if required.

## Example Nginx Configuration

### `nginx.conf`

```conf
http {
    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    keepalive_timeout  65;

    upstream socket_nodes {
        ip_hash;
        # IP Address of Host running Trudesk
        server x.x.x.x:8118;
    }

    server {
        listen 80;
        return 301 https://$host$request_uri;
    }

    server {
        listen       443;
        server_name  trudesk.domain.com;

        #ssl configuration
        ssl_certificate         /path/to/certificate.crt
        ssl_certificate_key     /path/to/certificate.key

        ssl on;
        ssl_session_cache builtin:1000 shared:SSL:10m;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_ciphers HIGH:!aNULL:!eNULL:!EXPORT:!CAMELLIA:!DES:!MD5:!PSK:!RC4;
        ssl_prefer_server_ciphers on;


        location ~ ^/(uploads/) {
                root /usr/src/trudesk/public;
                access_log off;
                expires modified +1h;
        }

        location / {
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
                proxy_http_version 1.1;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header Host $host;
                proxy_cache one;
                proxy_cache_key trudesk$request_uri$scheme;
                proxy_pass http://socket_nodes;

                proxy_redirect http://socket_nodes https://socket_nodes;
        }

        # redirect server error pages to the static page /50x.html
        # in the even that the trudesk instance is down, these pages will serve.
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
        }
    }
}
```