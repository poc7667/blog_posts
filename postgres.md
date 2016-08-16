---
title: PostgreSQL setting 
tags: DB
---

Notes for postgresql operation


<!-- more --> 

# Create User (Ubuntu)

    sudo su - postgres ; psql ;
    psql -d template1 -U postgres

# Change password
    
    ALTER USER "postgres" WITH PASSWORD 'jiyubiEzfly';
    ALTER USER "postgres" WITH PASSWORD 'ucscext123';
    \q


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

Dump database

    pg_dump -h localhost -U postgres -f alpa.dump AlphaLoan_production -Fc

Restore database

    pg_restore --verbose --clean --no-acl --no-owner -h localhost -U postgres -d AlphaLoan_production ./alpa.dump


PSQL configuration file location `/usr/local/var/postgres` 

    CREATE USER postgres WITH PASSWORD '<YOUR_PASSWORD>';
    ALTER USER postgres WITH SUPERUSER;


Login postgresql on ubuntu and change password

    sudo su - postgres ; psql
    ALTER USER "postgres" WITH PASSWORD 'alphaloan123';
    postgres=# ALTER USER "postgres" WITH PASSWORD 'alphaloan123';
    ALTER ROLE
    postgres=# \q


# md5 peer authentication 問題

you need to change the auth method from `peer` to `md5` to enable Rails can works.

    sudo vim  /etc/postgresql/9.5/main/pg_hba.conf
    sudo /etc/init.d/postgresql restart

# Forget password

Change the authtication method to peer


    sudo vim  /etc/postgresql/9.5/main/pg_hba.conf
    sudo /etc/init.d/postgresql reload    
    sudo su - postgres ; psql
    AND change ur password in the following steps

http://stackoverflow.com/questions/18664074/getting-error-peer-authentication-failed-for-user-postgres-when-trying-to-ge



SELECT *
FROM
    (
    SELECT
       *
       ,COUNT(*) OVER (PARTITION BY r.Id) as RoomDateCount
    FROM
       hotels h
       INNER JOIN rooms r
       ON h.Id = r.hotel_id
       INNER JOIN room_skus s
       ON r.id = s.room_id
       AND s.date BETWEEN '2016-08-12' AND '2016-08-18'
    ) t
WHERE
    t.RoomDateCount = DATE_PART('date', '2016-08-18' - '2016-08-12');