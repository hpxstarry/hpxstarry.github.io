---
title: 前端开发入门
date: 2020-03-04 00:31:10 -0800

categories: [Website]
tags: [vue]
seo:
  date_modified: 2020-03-20 23:40:26 -0700
---
>
前方高能，作者为表达方便，非常任性，想用中文就用中文，想用英文就用英文， 不喜误入。

虽然在软件开发行业已混迹多年，但对前端的了解甚少，只零零散散接触过ruby on rails, HTML5之类的。为成为一个全栈工程师，前端技术的了解必不可少。试着在网上搜寻相关的tutorial,然而并没有找到特别有用的资料。本博客将记录我从零开始学习前端的过程。希望本博客对同样想要学习前端的人有所帮助。

# 前端技术储备
前端必学三剑客
* HTML. 网页Mark up language，用于编辑网页内容。[资料](https://www.w3schools.com/html/default.asp)
* CSS. Cascading Style Sheets, 指明网页内容的style, 例如字体，背景等。常嵌入html中。 [资料](https://www.w3schools.com/css/)
* JAVASCRIPT. 前端的编程语言，常嵌入HTML中。用于与用户、后台交互，改变网页内容等。 [资料](https://www.w3schools.com/js/)

Javascript frameworks
* Anjular, developed by Facebook
* Vue.js
* React, developed by Google

Misc
* [Bootstrap](https://www.w3schools.com/whatis/whatis_bootstrap.asp) - 非常流行的CSS framework，适合于responsive和移动端网站。
* Typescript - super set of JavaScript with typed support. 
* JavaScriptX - entension of JavaScript. 
* jQuery - JavaScript library.  A lightweight, "write less, do more", JavaScript library.
  + HTML/DOM manipulation
  + CSS manipulation
  + HTML event methods
  + Effects and animations
  + AJAX - Asynchronous JavaScript and XML, is the art of exchanging data with a server, and updating parts of a web page - without reloading the whole page.

# 后端技术储备
* node JS

# 亲身实践
目标：在githug pages上建立一个网站，前端用VUE.JS。参考(博客)[https://blog.usmanity.com/serving-vue-js-apps-on-github-pages/]

1. set up (Windows)
  1. 安装 nvm-windows 作为 node.js 的版本管理器 https://github.com/coreybutler/nvm-windows
  1. 安装 cmder 作为WINDOWS下的shell
  1. 在 cmder shell中，运行"nvm install 13.12.0" 和 "nvm use 13.12.00" 来安装 node.js
  1. 在 cmder shell中，运行“npm install -g @vue/cli" 来安装vue-cli
2. github 创建repository
3. 