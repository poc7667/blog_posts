---
title: angular-cheatsheet
date: 2016-04-09 10:14:42
tags:
---

# Show un-safe string as HTML

Add a filter

    angular
        .module('altairApp').filter('unsafe', function($sce) {
        return function(val) {
            return $sce.trustAsHtml(val);
        };
    });

In the view

    <p ng-bind-html="product.description | unsafe"></p>


# Dropdown selection: single and multiple choice

## single choice

pitfalls
> {{$select.selected.name}} 

            <ui-select ng-model="user_profile.career" theme="bootstrap" required="true">
            <ui-select-match > {{$select.selected.name}} </ui-select-match>
            <ui-select-choices repeat="option in selectOptions.career | propsFilter: {name: $select.search} ">
            <div ng-bind-html="option.name | highlight: $select.search"></div>
            </ui-select-choices>
            </ui-select>

## multiple choice

pitfalls
> multiple, {{$item.name}}

            <ui-select multiple ng-model="loan_plan.careers" theme="bootstrap" ng-disabled="disabled">
            <ui-select-match > {{$item.name}} </ui-select-match>
            <ui-select-choices repeat="option in careersOptions | propsFilter: {name: $select.search} ">
            <div ng-bind-html="option.name | highlight: $select.search"></div>
            <small>
            <span ng-bind-html="''+ option.description | highlight: $select.search"></span>
            </small>
            </ui-select-choices>
            </ui-select>

# DEBUG skill

Check the existence of service on the console

> injector = angular.element(document.body).injector()
> injector.get('ServiceName')
    angular.js:68 Uncaught Error: [$injector:unpr] Unknown provider: ServiceNameProvider <- ServiceName(…)(anonymous function) @ angular.js:68(anonymous function) @ angular.js:4289getService @ angular.js:4437(anonymous function) @ angular.js:4294getService @ angular.js:4437(anonymous function) @ VM168822:1InjectedScript._evaluateOn @ (program):878InjectedScript._evaluateAndWrap @ (program):811InjectedScript.evaluateOnCallFrame @ (program):936(anonymous function) @ banks.js:2


# RESTful

success callback

error callback


