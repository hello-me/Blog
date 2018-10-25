---
title: 关于Vue.js的单元格测试
date: 2018-10-15 15:51:10
tags: vue.js
---
### 前言
vue.js是一个构建web应用程序的前端框架，对于每个项目，有必要在我们的应用程序中查看所有的内容，对于大型项目
来说，每次有新的更新后，检查每个功能就变得很麻烦且费时间，因此，我们可以创建一直运行的自动化检测，保证我们的代码可以正常运行。
### 搭建环境
 首先我们需要用vue-cli搭建一个vue项目
> npm install -g vue-cli
> vue init webpack vuetest

在这个阶段会被提示几个问题，可以根据自己的需要去选择
![](t.png)
但是红框框起来的Set up unit tests 一定要选yes
及 pick a test runner 要选择 Karma and Mocha
然后安装依赖，最终使用npm run dev 运行项目
接下来输入以下命令，给项目安装karma-chrome-launcher和vue-test-utils
> npm install karma-chrome-launcher --save-dev
> npm install --save-dev vue-test-utils

然后在项目中找到test/unit/karma.conf.js文件，将将PhantomJS浏览器修改为Chrome，因为PhantomJS会经常莫名其妙报好多错
![](C.png)
### 第一次单元测试
当完成以上步骤后, 就可以在命令行输入 npm run unit 来启动第一次单元测试，vue脚手架已经初始化了一个HelloWorld.spec.js的测试文件去测试HelloWrold.vue
在test/unit/specs/HelloWorld.spec.js就可以就可以看到这个文件(所有的测试文件, 都将放specs这个目录下, 并以测试脚本名.spec.js结尾命名)
输入 npm run unit 看到这样的情形就说明成功了
![](test.png)
### Mocha进行同步测试demo
首先先写一个vue文件如test.vue然后在test/unit/specs/下添加一个test.spec.js文件
test.vue内容如下
![](vue.png)
test.spec.js内容如下
![](testjs.png)
再次在命令行输入npm run unit就会看到
![](1.png)
说明测试成功了
demo中使用了Mocha框架写测试脚本
Mocha的作用是运行测试脚本, 要对上面Counter.vue进行测试, 我们就要写测试脚本, 通常测试脚本应该与Vue组件名相同, 后缀为spec.js. 比如, Counter.vue组件的测试脚本名字就应该为Counter.spec.js
测试脚本代码中，包含一个或者多个describe,每个describe块应该包括一个或者多个it块
#### describe
describe块称为"测试套件"，表示一组相关的测试，他其实是一个函数，第一个参数就是测试套件的名称(例子中就是test.js)
第二个参数就是一个实际执行的函数
#### it
it块称为"测试用例"表示一个单独测试，就是一个测试最小的单位，他也是一个函数，第一个参数是测试用例的名称(通常描述你的断言结果，比如demo中是'点击按钮后，内容会发生改变')
第二个参数就是一个实例执行的函数
#### expect
上面的demo中，以expect()方法开头的就是断言。
断言就是判断源代码的实际执行效果与预期的是否一致，如果不一致就会抛出错误，断言库有很多种，Mocha并不限制你需要使用哪一种断言库
Vue的脚手架提供的断言库是sino-chai，是一个基于Chai的断言库，并且我们指定使用的是它的expect断言风格。
每一个it()所包含的测试用例都应该有一句或者多句断言。Chai有很多的断言语法，想知道其他的可以看看官方文档
[Chai官方文档](http://chaijs.com/)  
[Chai官方文档翻译](http://www.jianshu.com/p/f200a75a15d2)
[阮一峰 - 测试框架 Mocha 实例教程 ](http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html)
### Mocha进行异步测试demo
现在在原来test.vue文件上加上一个异步自增的函数
![](2.png)
在test.spec.js文件上加上一个新的测试用例就是it()
![](3.png)
输入npm run unit看到如下信息说明异步测试成功
![](4.png)
Mocha中的异步测试，需要给it()内函数的娴熟中添加一个done,并在意不执行完成后必须调用done(); 如果不调用done(),nameMocha会在2000s
后报错并且本次单元测试失败（mocha默认的异步测试超时上线为2000ms）
### Vue-test-utils
刚才一开始就安装了Vue-test-utils这个库，但是一直没用，现在看看用这个库来测试有多方便
这是一个使用Vue-test-utils异步测试的demo
![](5.png)
对比一下上图，代码量是不是少了很多，如果是更复杂的测试用例，那么代码减少量将更为突出。
运行npm run unit可以看到测试成功了
![](6.png)
接下来我们看下vue-test-utils简单的API
.find():返回匹配选择器的第一个DOM节点或Vue组件的wrapper,可以使用任何有效的选择器
.text():返回wrapper的内容
.html():返回wrapper DOM的HTML字符串
.trigger():在该wrapper DOM节点上触发一个事件
.setData():设置data的属性并强制更新
要具体学习的话可查看[官方文档](https://vue-test-utils.vuejs.org)


