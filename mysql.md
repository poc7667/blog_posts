---
title: MySQL configuration
tags: database
---

# Forget the root password (OSX)


    mysql.server stop
    mysql.server start --skip-grant-tables 
    mysql
    mysql> use mysql;
    mysql> UPDATE user SET password=PASSWORD('YOUR_NEW_PASSWORD_HERE') WHERE user = 'root';
    mysql> exit;
    mysql.server stop
    mysql.server start