---
title: angular-pattern
date: 2016-04-09 10:14:42
tags: angular
---

- Router '/app/dashboard-v1' ->  State 'app.dashboard-v1'
- Router '/app/ui' ->  State 'app.ui'

# snippet

          $urlRouterProvider
              .otherwise('/app/dashboard-v1');
          $stateProvider
              .state('app.ui', {
                  url: '/ui',
                  template: '<div ui-view class="fade-in-up"></div>'
              })
              .state('app.ui.buttons', {
                  url: '/buttons',
                  templateUrl: 'tpl/ui_buttons.html'
              })

ui-router的状态

參考 http://blog.csdn.net/mooner_guo/article/details/42459861

Parent state 以及 children state 依靠 "." 區分 namespace

 > question : patent state
 > question.init.attention.text : 子狀態children state
 > 

      $stateProvider.state('question',{     //母模块
                ....
          }).state('question.init.attention.test',{       //子状态1  显示view1
                  url:"/test",
            views:{
                /*'first':{
                    template:'<div>first</div>'
                },*/
                'second':{
                    template:'<div>second</div>'
                }
         }).state('question.init.attention.test',(        //子状态2 显示view2
                   url:"/test2",
            views:{
                'first':{
                    template:'<div>first</div>'
                }
                /*'second':{
                    template:'<div>second</div>'
                }*/
            }
         )}.state('question.init.attention.test',{       //子状态3    显示view1，view2
             url:"/test2",
            views:{
                'first':{
                    template:'<div>first</div>'
                }
                'second':{
                    template:'<div>second</div>'
                }
            }
        });


# Abstract

Abstract - {boolean=} - An abstract state will never be directly activated, but can provide inherited properties to its common children states.

          $stateProvider
              .state('loan', {
                  abstract: true,
                  url: '/loan',
                  templateUrl: 'tpl/app.html'
              })
              .state('loan.loan_manager', {
                  // abstract: true,
                  url: '/loan_manager',
                  templateUrl: 'tpl/ui_buttons.html'
              })