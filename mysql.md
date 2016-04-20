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



# login on ubuntu

    mysql -u root -p

# find the pid file location

    mysqladmin -uroot -p<ROOT_PASSWORD> variables | grep sock

# change pid file location
    
edit /etc/mysql/my.cnf

    socket = /tmp/mysqld.sock
    pid-file = /tmp/mysqld.pid


# Unable to lock ./ibdata1, error: 11


# cheatsheet

    - https://gist.github.com/poc7667/3850d140df135106fefcd44532f6837f

    - http://blog.toright.com/posts/1145/mysql-%E6%94%B9-root-%E5%AF%86%E7%A2%BC%E5%BF%85%E5%8B%9D%E6%96%B9%E6%B3%95%EF%BC%88%E7%AD%86%E8%A8%98%EF%BC%89.html