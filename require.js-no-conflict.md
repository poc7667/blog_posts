---
title: Avoid included jQuery pollutes global jQuery
date: 2016-05-15 15:45:48
tags: Javascript, require.js
---

先前遇到了一個問題，我用 require.js build 一個 js plugin

想不到在客戶的網站裡面，因為該客戶已經 include 一個非常舊版本的 jQuery
然後被我包出來的 plugin 裡面自帶(self-included) 蓋掉，

導致對方的其他 scripts 接連受影響。

This post tells how to avoid polluting the existing global jquery with your require.js project.

Create a file under project root `require_no_conflict_jquery.js`

    define( ["jquery"], function(jq) {
        // Raw jQuery does not return anything, so return it explicitly here.
        return jQuery.noConflict( true );
    } );

# app.main.js

    requirejs.config({
        paths: {
            jq_no_conflict: "require_no_conflict_jquery",
            jquery: "./vendor/js/jquery-2.1.1.min",
        },
        map: {
            '*': {
                'jquery': 'jq_no_conflict'
            },
            'jq_no_conflict': {
                'jquery': 'jquery'
            }
        },

# app.build.js

    {
        mainConfigFile: 'app.main.js',
        out: "../js/dadasay.noJQConflict.min.js",
        optimize: "none",
        preserveLicenseComments: false,
        wrap: true,
        paths: {
            requireLib: './require'
        },
        include: [ 'requireLib', 'app.main.js' ],
        // insertRequire: ["app.main"],
    }

#Build it

    r.js -o app.build.js