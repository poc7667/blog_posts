---
title: angular interacts with DOM and FB plugin
date: 2016-04-15 10:14:42
tags: angular
---

最近需要讓　Angular 與　FB share button 互動，

想要達成的目標是當我的　URL 一有更動，　FB share button 的連結(href) 也要跟著動。

# cheatsheet

    FB.XFBML.parse(); // 重新render, compiple FB button plugin
    $location.$$absUrl, $location.url() 拿到你當前的　url

    // compile 新的 DOM 元件
    $('#quick_search_btn').append($compile(share_btn_dom)($rootScope));

    // 放到　$timeout 避免遇到跟正在進行　digest phase conflict 的issue
    $timeout(function(){
       $rootScope.$apply();
     });

# Invaliad Pattern

一開始我嘗試要在　app.run　裡面綁一個　`$locationChangeSuccess` callback,

然後　remove 原本的　fb btn dom, 再　insert 新的　fb btn dom, 

遺憾的是，完全沒有反應 (這邊我推測我違反了　Angular data flow 的　life cycle 所以會一點作用都沒有)

# Facebook

      $scope.fbShareBtnTemplate = '<div class="fb-share-button" data-href="'+ targetUrl+ '" data-layout="icon_link" data-mobile-iframe="true""> </div>　'
