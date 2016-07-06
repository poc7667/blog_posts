---
title: JS debugger CheatSheet
date: 2016-07-03 10:14:42
tags: javascript
---

# Embed errorception  into your website

You'll never know where an exception happens on the client side.

JS除錯第三方的好工具，客戶端的環境千百種，靠開發窮舉測試幾乎是不可能的任務。

Simply illustrate how to install it on an Angular js project.

Put the snippet at the every page's header section.
Make it be executed as soon as possible.


<!-- more --> 




    +        <!-- ErrorException -->
    +        <script>
    +            (function(_,e,rr,s){_errs=[s];var c=_.onerror;_.onerror=function(){var a=arguments;_errs.push(a);
    +            c&&c.apply(this,a)};var b=function(){var c=e.createElement(rr),b=e.getElementsByTagName(rr)[0];
    +            c.src="//beacon.errorception.com/"+s+".js";c.async=!0;b.parentNode.insertBefore(c,b)};
    +            _.addEventListener?_.addEventListener("load",b,!1):_.attachEvent("onload",b)})
    +            (window,document,"script","5776cCXCCX7900024c");
    +        </script>


`Angular integration`: open up an angular config file make sure your module name called `app`, and inject this snippet.

    +app.config(function($provide) {
    *  $provide.decorator("$exceptionHandler", ['$delegate', function($delegate) {
    *    return function(exception, cause) {
    *      _errs.push(exception);
    *      $delegate(exception, cause);
    *    }
    *  }])
    +});


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






