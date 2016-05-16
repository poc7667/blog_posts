---
title: PostgreSQL setting 
tags: DB
---

遇到新舊版DB衝突，通常升級資料庫之後會遇到

    FATAL:  database files are incompatible with server
    DETAIL:  The data directory was initialized by PostgreSQL version 9.3, which is not compatible with this version 9.5.1.
    launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist


Backup the old DB store and create a new one.

    mv /usr/local/var/postgres /usr/local/var/postgresOLD
    initdb /usr/local/var/postgres

If you want to start the DB on boot

    cp /usr/local/Cellar/postgresql/<VERSION>/homebrew.mxcl.postgresql.plist ~/Library/LaunchAgents/
    eg: cp /usr/local/Cellar/postgresql/9.5.1/homebrew.mxcl.postgresql.plist ~/Library/LaunchAgents

