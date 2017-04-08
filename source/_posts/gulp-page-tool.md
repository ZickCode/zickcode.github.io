---
title: gulp自动化脚手架
date: 2017-04-08 20:29:19
tags: gulp
---

在学习gulp的过程中，使用gulp搭建了一个前端自动化开发的脚手架，期间参考过网上许多大神已有的例子，拜谢
还有很多可以完善的地方，欢迎批评指正

##### 项目地址
https://github.com/ZickCode/gulp-page-tool

##### 使用优化
使用yeoman配置了generator，可以使用yo命令自动生成初始化文件及目录配置
https://github.com/ZickCode/generator-pageTool

##### 基本功能
#### 1.css
使用less，自动编译为css
css合并为两个文件：main.css，plugins.css，
引入了reset.css用来重置浏览器样式，animate.css动画库，
使用gulp-autoprefixer处理浏览器兼容
#### 2.js
js合并为三个文件：页面main.js，第三方库vendor.js，各类插件plugins.js
页面顺序为vendor>plugins>main
使用gulp-uglify压缩和gulp-babel转换为ES5
#### 3.image
使用gulp-image-min进行图片压缩，压缩率感人，如果图片过大还是推荐手动使用各类在线图片压缩网站或者压缩软件
#### 4.本地开发
使用browser-sync搭建本地预览服务器，可以设置PC和移动端同步操作
#### 5.版本控制
使用gulp-rev和gulp-rev-collector在文件名后追加md5版本号，以处理静态资源缓存问题
可改用gulp-rev-append在不修改文件名的情况下以?rev=@@hash方式处理缓存，需要在gulpfile.js和页面里配置