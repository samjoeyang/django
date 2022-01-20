# html模版页面配置

1.  内容标签 &#x20;

    ```markup
     <div class="col-lg-8 col-lg-offset-2 col-md-10 col-md-offset-1">
       {% block content %}{% endblock %}
     </div>
    ```
2.  导航条 &#x20;

    ```markup
    <ul class="nav navbar-nav navbar-right">
    {% show_menu 0 0 100 100 %}
    </ul>
    ```
3.  配置内容区域,主要是添加占位符`{% placeholder "content" %}`,在templates文件夹下面，新建一个content.html文件，将以下内容复制进去

    ```
    {% extends "base.html" %}
    {% load cms_tags %}

    {% block content %}
        {% placeholder "content" or %}{%endplaceholder%}
    {% endblock content %}
    ```


4.  django CMS占位符的高级使用 `or %}`的标签的意思是，占位符没有内容输出的时候，你可以通过`or %}`来定义显示的内容。如果占位符没有内容输出，我们让它显示about-bg.jpg。

    ```markup
    <!-- Page Header -->
    {% placeholder header or %}
    <header>...about-bg.jpg...</header>
    {%endplaceholder%}
    ```
5.  配置文章标题，使用{% page\_attribute "page\_title" %}这个模板标签,可以通过Page > Page Settings来修改这个标题。 &#x20;

    将以下的代码： &#x20;

    ```markup
    <div class="page-heading">
     <h1>About Me</h1>
     <hr class="small">
     <span class="subheading">This is what I do.</span>
    </div>
    ```

    修改成这样：

    ```markup
    <div class="page-heading">
     <h1>{% page_attribute "page_title" %}</h1>
    </div>
    ```

