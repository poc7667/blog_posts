---
title: back-up-databases
date: 2016-07-17 11:14:27
tags:  devops
---

To back-up our databases periodically.

References: http://backup.github.io/backup/v4/getting-started/ 


<!-- more --> 


Suppose our database is `postgresql`

    backup generate:model --trigger backupAlphaLoan --databases="postgresql" --storages="local" --compressor="gzip"

    backup perform --trigger backupAlphaLoan

