---
title: AWS
tags: aws
---

- add another aws configure

eg: assign a new profile name

> aws configure --profile ezfly


- use direnv to load a different aws profile


- ssh login without pem file

open `/etc/ssh/sshd_config`

Before
> PasswordAuthentication no

After

> PasswordAuthentication yes

change PasswordAuthentication no to PasswordAuthentication yes
