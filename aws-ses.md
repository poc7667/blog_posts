---
title: aws-ses
date: 2016-07-21 09:28:46
tags: AWS
---

# Setting of AWS SES

Do not contain `smtp` in the server address [Ref](https://github.com/drewblas/aws-ses/issues/60)

    email-smtp.eu-west-1.amazonaws.com ->  email.eu-west-1.amazonaws.com

# Register a new domain  on SES

![inline](https://i.imgur.com/qdEEaMD.png=300x "Title")

If you're using Route 53 for hosting your domain, you can simply click the "Route 53" button on the bottom of the page. It will automatically configure the setting for you.
![inline](https://i.imgur.com/BX3nH2F.png=300x "Title")

# Register email

In the sandbox environment, you're only able to send mail to the verfied users.

![inline](https://i.imgur.com/hi88YGk.png=300x "Title")

# Get your SMTP setting and credential

![inline](https://i.imgur.com/FtD3SU2.png=300x "Title")


        ActionMailer::Base.smtp_settings = {
            :address => ENV["SES_SERVER"],
            :port => "587",
            :domain => "jiyubi.com",
            :user_name => ENV["SES_USER"],
            :password => ENV["SES_PASSWORD"],
            :authentication => "plain",
            :enable_starttls_auto => true
        }

# References

[一年免費玩盡 Amazon 雲端服務 – 低成本 EDM 電郵服務](http://www.hkitblog.com/?p=24711)