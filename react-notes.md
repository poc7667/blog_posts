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



