---
title: python-crawler-notes
date: 2016-03-21 10:09:08
tags: Python
---

記錄 Python 爬蟲的零碎筆記

# Create a requests object with session

有時候需要 session 去記錄每一步 request , Server回傳給我們的 response (header, cookie)

import requests
