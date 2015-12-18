---
layout: post
title:  Gulp：编译CoffeeScript
date:   2015-12-07 08:24:00
category: [Gulp]
tags: [Gulp,CoffeeScript]
---

从编译CoffeeScript看Gulp的使用

本文环境:

- npm
- Ubuntu

<!--more-->

## 安装CoffeeScript

    sudo npm install -g coffee-script

## 安装Gulp
官网只有第一句,但是这样是不能找到gulp,所以两句都要执行:

    sudo npm install --global gulp
    sudo npm install gulp

## 给项目初始化npm配置

    sudo npm init
    
根据提示配置好package.json,大概这样:

    {
      "name": "EasyCanvas",
      "version": "0.0.0",
      "description": "A HTML5 canvas library based on pure JavaScript",
      "main": "EasyCanvas.js",
      "directories": {
        "test": "test"
      },
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "repository": {
        "type": "git",
        "url": "https://github.com/younglaker/EasyCanvas.git"
      },
      "author": "Laker Huang",
      "license": "MIT",
      "bugs": {
        "url": "https://github.com/younglaker/EasyCanvas/issues"
      }
    }

## 安装gulp-coffee

[gulp-coffee][1] : Coffeescript plugin for gulp 

可以全局安装

    sudo npm install --global gulp-coffee

也可以只安装到本目录,并且添加信息到package.json里:

    sudo npm install --save gulp-coffee


## 安装gulp-util

[gulp-util][2] : Utilities for gulp plugins .

    sudo npm install --save gulp-util
    
## 配置gulp
在项目里建个gulpfile.js:

    var gulp = require('gulp');
    var coffee = require('gulp-coffee');
    var gutil = require('gulp-util');
    
    gulp.task('default', function() {
      // 默认的任务代码
    });
    
    gulp.task('coffee', function() {
      gulp.src('./coffee_directions/*.coffee')
        .pipe(coffee({bare: true}).on('error', gutil.log))
        .pipe(gulp.dest('./js_directions/'))
    });

执行coffee任务

    gulp coffee

  [1]: https://github.com/contra/gulp-coffee
  [2]: https://github.com/gulpjs/gulp-utilhub.com/contra/gulp-coffee