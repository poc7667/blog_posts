---
title: nginx-cheat-sheet
date: 2016-07-19 15:44:51
tags: Nginx
---

# Sections

- basic auth

# basic auth (Set Up Password Authentication with Nginx on Ubuntu 14.04)

install  `apache2-utils` first

    sudo apt-get install apache2-utils

cd to `/etc/nginx`

    htpasswd -c .htpasswd deploy

Nginx.conf

    server {
          listen 3000;
          server_name www.sample.co sample.co;
          location / {
              auth_basic "Restricted";
              auth_basic_user_file /etc/nginx/.htpasswd;  #For Basic Auth
          }
    }
