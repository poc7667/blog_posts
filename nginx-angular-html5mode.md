---
title: nginx-angular-html5mode
date: 2016-08-10 20:49:03
tags:
---

This code is about how to turn on the HTML5 mode on Angular js and rewrite the request on Nginx side.


# Angular side

Remeber to put `<base href="/">` before including any js file.


# Nginx

     location / {
       auth_basic "Restricted";
       auth_basic_user_file /etc/nginx/.htpasswd;  #For Basic Auth
+      try_files $uri $uri/ /index.html ; # make HTML5 workable
+
     }
