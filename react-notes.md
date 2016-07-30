---
title: react-course-notes
date: 2016-07-12 18:42:44
tags: React
---

Prop 是constant 的角色, state 的子集合

所以要改變子孫的 prop, 就從最上層的 container 開始改變。

向下傳遞的除了資料流以外也可以是

one way 資料流： (dispatcher) -> (store) -> (view) -> (action) ----> (dispatcher)


<!-- more --> 

# 2016-07-26

Good practice.

盡量保持 stateless.

你也可以只建立一個 parent component, 只用來負責 hold states, 不用來畫也可以。

component lifycycle:

這邊提到的 mount willMount 說的是 mount 到 VDOM

大多時間都會在 didMount 做事情，因為這個callback才會 trigger re-render.
(記住，都只是在 VDOM 操作，不要養成 reail dom)


Will mount (從ROOT 觸發到 leaf)
Did mount ( leaf 回傳到 root), leaf 最先trigger 在把 callback 傳回給root

## Immutability

不要嘗試去 modify state, 直接 creat new array and replace the old one

## data flow 概念

通常 remote-api-interaction 不要四散在各地的componest, 集中在 top 執行。

通常 action 會在 leaf 觸發，一個 checkbox 之類 在一路的calback 到root




# material

Text book: pro react

練習  project https://github.com/jiayihu/react-kanban

# 建立環境

## React hello world example

- [React hello world](https://gist.github.com/danawoodman/9cfddb1a0c934a35f31a)
- [Reac reduc quick start](https://github.com/starkwang/react-redux-es6-quickstart)


        npm init -y  # -y 就是不要問，一切給我按照預設
        npm i --save-dev css-loader style-loader webpack-dev-server
        npm install -g babel-loader react react-dom react-redux redux redux-devtools react react-dom babelify babel-preset-react react react-dom babel-preset-react babel-loader babel-core
        npm install --save react react-dom  webpack babel-core babel-loader babel-preset-react babel-preset-es2015 babel-polyfill



## Syntax notes


return 不能一次同時傳回多個 nodes, 如果非要這樣做不可 請用 div 把它包起來。

要trigger render 就是呼叫 `this.setState(OBJ)`, 千萬不能使用 this.state.name = "Poc" , 這樣子不會 call re-render



