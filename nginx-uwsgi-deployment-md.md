---
title: Nginx uwsgi deployment notes
date: 2015-11-24 16:58:41
---

We're going to show how to ind

Firstly, run [setup requirements recipe](https://gist.github.com/poc7667/03aa32518f5962c0c2bc) for instaling required packages

I am used to using `capistrano` for auto deployment

Install the deployment config files under project folder
>
cap install

Because the deployment files could be large, 

I won't put them under root disk to avoid no space on the disk issue, 

I usually mount a external disk and deploy onto it.

mount the external disk to /workspace
mkdir /workspace/deploy_workspace

I usually put all the deploy

Avoid to run out of the root disk volume space,

We should change the DB datastore location to external disk.

Please refer to [this snippet](https://gist.github.com/poc7667/628a8a467d6dcd704b29) for setting up MongoDB


最好把python 相關的 packages 以 system 的方式安裝
因為 Foreman 在執行的時候不會 跑 pyenv 的 python 而是 system python