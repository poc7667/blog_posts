---
title: angular-course-notes
date: 2016-07-13 19:26:14
tags: angular
---

理解 Javascript 裡面的 event loop 異步操作的原理

- [JavaScript 运行机制详解：再谈Event Loop](http://www.ruanyifeng.com/blog/2014/10/event-loop.html)
- [Philip Roberts: What the heck is the event loop anyway? | JSConf EU ](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

# 2016-07-20

ES6 + Webpack 開發 Angular

xnpm install -g gulp karma karma-cli webpack


# 2016-07-13

利用 `ng-class` 動態地元件上style


## ng controller for

        <script>
            angular.module("exampleApp", [])
                    .controller("defaultCtrl", function ($scope) {
                        $scope.settings = {
                            Rows: "Red",
                            Columns: "Green"
                        };
                    });
        </script>
        <style>
            tr.Red { background-color: lightcoral; }
            tr.Green { background-color: lightgreen;}
            tr.Blue { background-color: lightblue; }
        </style>
        <table class="table">
            <thead>
            <tr><th>#</th><th>Action</th><th>Done</th></tr>
            </thead>
            <tr ng-repeat="item in todos" ng-class="settings.Rows">
                <td>{{$index + 1}}</td>
                <td>{{item.action}}</td>
                <td ng-style="{'background-color': settings.Columns}">
                    {{item.complete}}
                </td>
            </tr>
        </table>