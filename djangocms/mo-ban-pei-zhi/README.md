---
description: >-
  模版配置分两大部分：1、针对DjangoCMS工具栏的配置，后面工具栏是很有用处的；2、针对html文件的页面上内容的配置，主要是标签配置、占位符配置、导航条配置和常量显示
---

# 模版配置

总的原则如下：

1. 把模版的css、js、images等文件或目录复制到项目同名的应用目录下的static文件夹下面,可以创建自己的目录，如“unoecp” &#x20;
2.  在模版的页面文件头部（第一行或者第二行）添加 &#x20;

    `{% load staticfiles i18n cms_tags sekizai_tags menu_tags %` &#x20;
3.  修改css文件路径,格式如下 &#x20;

    `<link href="{% static 'unoecp/css/main.min.css' %}" rel="stylesheet">` &#x20;
4.  修改js文件路径,格式如下 &#x20;

    `<script src="{% static 'unoecp/js/jqBootstrapValidation.js' %}"></script>`
5.  修改静态图片路径,格式如下 &#x20;

    `<header class="intro-header" style="background-image: url({% static 'unoecp/img/about-bg.jpg' %})">` &#x20;
6.  其他静态资源，格式参考如下 &#x20;

    `{% static 'folder1/folder2/filename.ext' %}` &#x20;



参考：[蜗牛博客](http://www.snailtoday.com/archives/7652)







### **CMS的配置**

#### ****
