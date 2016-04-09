---
title: commands-snippets
date: 2015-12-14 16:22:16
---


### Replace of a string recursively under a specific folder

if the string contains  double quote `"` you should escape it by backslash

This example will replace `version: "0.0.2"` to `version: "1.0.0"`

    find <SPECIFIC_FOLDER> -type f -print0 | xargs -0 sed -i '' 's/version: \"0.0.2/version: \"1.0.0/g'
