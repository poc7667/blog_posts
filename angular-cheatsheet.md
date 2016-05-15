---
title: angular-cheatsheet
date: 2016-04-09 10:14:42
tags:
---

# DEBUG skill

Check the existence of service on the console

> injector = angular.element(document.body).injector()
> injector.get('ServiceName')
    angular.js:68 Uncaught Error: [$injector:unpr] Unknown provider: ServiceNameProvider <- ServiceName(…)(anonymous function) @ angular.js:68(anonymous function) @ angular.js:4289getService @ angular.js:4437(anonymous function) @ angular.js:4294getService @ angular.js:4437(anonymous function) @ VM168822:1InjectedScript._evaluateOn @ (program):878InjectedScript._evaluateAndWrap @ (program):811InjectedScript.evaluateOnCallFrame @ (program):936(anonymous function) @ banks.js:2


# RESTful

success callback

error callback