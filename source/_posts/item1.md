---
title: 如何搭建vue框架
tags: [Vue, Vue-cli]
---

1.首先安装node,借助node的npm来安装依赖包。（如果直接使用npm安装，可能很慢，可以使用淘宝的npm镜像：
输入npm install -g cnpm –registry=https://registry.npm.taobao.org，即可安装npm镜像，以后直接用cnpm来代替npm）
2.安装完npm镜像后，开始安装vue-cli脚手架，输入cnpm install -g vue-cli，验证是否安装成功，在命令行中找到该项目后输入vue，有vue的信息出来则安装成功。
3.安装完脚手架以后开始，开始创建一个新项目（new_project）：命令 vue init webpack new_project  （创建一个基于"webpack"的项目，后面是项目名）
4.一个新的项目文件夹就创建完成，这个项目结构里面会多出一个node_modules的文件夹，里面就是刚才安装的所有依赖。（后期项目需要什么依赖包，可通过cnpm install **来安装）
5.运行测试，在命令行中输入cnpm run dev，（8080就是默认的端口），一般浏览器会自动跳转出界面http://localhost:8080/，也可以手动打开流览器器输入地址。