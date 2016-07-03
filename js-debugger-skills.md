---
title: JS debugger skills
tags: javascript
---

# Expand objects in array

Paste this function to the chrome dev tool console

then pp(`The array you wanna show`)

        var pp = (function(){
            var MAX_DEPTH = 100;
            return function(item, depth){
                depth = depth || 0;
                if (depth > MAX_DEPTH ) {
                    console.log(item);
                    return;
                }
                if (_.isObject(item)) {
                    _.each(item, function(value, key) {
                    console.group(key + ' : ' +(typeof value));
                    pp(value, depth + 1);
                    console.groupEnd();
                    });
                } else {
                    console.log(item);
                }
            }
        })(); 






