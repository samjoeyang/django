# 写在前面的注意事项

Django的框架下都是以一个个的应用（app）形式呈现，但是总的是在项目（project)下的，而项目下存在一个跟项目同名的应用，所以行文中对于同名的项目和应用的区别可能没有照顾周全，初学者还是要注意一下。一般情况项目的树形结构如下：

例如：项目名称为：unoecp &#x20;

```
unoecp
 |-unoecp
 |   |-static
 |   |-templates
 |   |-__init__.py
 |   |-asgi.py
 |   |-settings.py
 |   |-urls.py
 |   |-views.py
 |   |-wsgi.py
 |-app1
 |   |-__init__.py
 |   |-admin.py
 |   |-apps.py
 |   |-models.py
 |   |-test.py
 |   |-urls.py
 |   |-views.py
 |-app2
 |   |-__init__.py
 |   |-admin.py
 |   |-apps.py
 |   |-models.py
 |   |-test.py
 |   |-urls.py
 |   |-views.py

```
