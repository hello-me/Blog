---
title: 'create-react-app脚手架 '
date: 2018-08-31 13:24:51
tags: React Yarn
---
### React 介绍
 React是Facebook研发的一款前端框架(MVC框架: 侧重于view层操作)，目前被广泛使用
### React脚手架create-react-app介绍
 为了快速地进行构建使用 React 的项目，FaceBook 官方发布了个无需配置的、用于快速构建开发环境的脚手架工具 create-react-app
 create-react-app所创建的应用入口文件是src/index.js文件。
#### 使用原因以及特性:
 .无需配置
 .集成了对React, JSX, ES6和Flow的支持；
 .集成了开发服务器；
 .配置好了浏览器的热加载的功能;
 .在javaScript中可以直接使用import CSS和图片;
 .自动处理CSS的兼容问题，无需添加-webkit前缀;
 .集成好了编译命令，编译后直接可以发布成产品，并且还包含了sourcemaps。
#### 安装和使用create-react-app
 > npm install -g create-react-app //注意需要添加 g 参数进行全局安装以及权限的问题                                
 > create-react-app my-app // my-app 就是你项目的名称
 > cd my-app
 > npm start
 
 在使用create-react-app脚手架的过程中要注意确保你的电脑上Node版本大于等于4。
 #### 关于yarn
 在初始化项目时我们需要npm install,或者在安装一些插件的时候需要用到npm,
 但是npm install 很慢，而且在开发项目要添加依赖的时候，用 npm 拉取依赖时，即使用的是相同的 package.json，在不同的设备上拉到的 packages 版本不一，这就可能为项目引入 bug
 为了防止拉取到不同的版本，Yarn 有一个锁定文件 (lock file) 记录了被确切安装上的模块的版本号。每次只要新增了一个模块，Yarn 就会创建（或更新）yarn.lock 这个文件。这么做就保证了，每一次拉取同一个项目依赖时，使用的都是一样的模块版本。
 所以用yarn可以减少bug，加快安装依赖的速度。
 ##### 什么是Yarn
 Yarn 是新一代包管理工具
 
 ##### 为什么使用Yarn
  - 速度快
  - 安装版本统一，更安全
  - 更简洁的输出
  - 更好的语义化
  
##### 如何使用Yarn
  - yarn init
  - yarn add
  - yarn remove
  - yarn install
 
 
                            
