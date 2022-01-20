# 初始数据的自动导入

原文链接：[https://wiki.jikexueyuan.com/project/django-chinese-docs-1.8/2-6-3-providing-initial-data.html](https://wiki.jikexueyuan.com/project/django-chinese-docs-1.8/2-6-3-providing-initial-data.html)

## 为模型提供初始数据

当你首次建立一个应用的时候，为你的数据库预先安装一些硬编码的数据，是很有用处的。 有几种方法可以让Django自动创建这些数据：你可以通过fixtures提供初始数据，或者提供一个包含初始数据的sql文件。

通常来讲，使用fixtrue更加简洁，因为它是数据库无关的，而使用sql初始化更加灵活。

### 提供初始数据的fixtures <a href="#bae53da1c108058d06826a0a43e10449" id="bae53da1c108058d06826a0a43e10449"></a>

fixture是数据的集合，让Django了解如何导入到数据库中。创建fixture的最直接的方式，是使用manage.py dumpdata命令，如果数据库中已经有了一些数据。或者你可以手写fixtures。fixtures支持JSON、XML或者YAML（需要安装PyYAML）文档。序列化文档中详细阐述了每一种所支持的序列化格式。

下面这个例子展示了一个简单的Person 模型的fixtrue，看起来很像JSON：

```
[
  {
    "model": "myapp.person",
    "pk": 1,
    "fields": {
      "first_name": "John",
      "last_name": "Lennon"
    }
  },
  {
    "model": "myapp.person",
    "pk": 2,
    "fields": {
      "first_name": "Paul",
      "last_name": "McCartney"
    }
  }
]
```

下面是它的YAML格式：

```
- model: myapp.person
  pk: 1
  fields:
    first_name: John
    last_name: Lennon
- model: myapp.person
  pk: 2
  fields:
    first_name: Paul
    last_name: McCartney
```

你可以把这些数据储存在你应用的fixtures目录中。

加载数据很简单：只要调用manage.py loaddata \<fixturename>就好了，其中\<fixturename>是你所创建的fixture文件的名字。每次你运行loaddata的时候，数据都会从fixture读出，并且重复加载进数据库。注意这意味着，如果你修改了fixtrue创建的某一行，然后再次运行了 loaddata，你的修改将会被抹掉。

### 自动加载初始数据的fixtures <a href="#0a01c3e6253d4331dca11e68fce57aaa" id="0a01c3e6253d4331dca11e68fce57aaa"></a>

```
1.7中废除：

如果一个应用使用了迁移，将不会自动加载fixtures。由于Django 1.9中，迁移将会是必要的，这一行为经权衡之后被废除。 如果你想在一个应用中加载初始数据，考虑在数据迁移中加载它们。
```

如果你创建了一个命名为 initial\_data.\[xml/yaml/json]的fixtrue，在你每次运行migrate命令时，fixtrue都会被加载。这非常方面，但是要注意：记住数据在你每次运行migrate命令后都会被刷新。So don’t use initial\_data for data you’ll want to edit.

### Django在哪里寻找fixture文件 <a href="#e7173725ca486ccca0e0190b4c797f26" id="e7173725ca486ccca0e0190b4c797f26"></a>

通常，Django 在每个应用的fixtures目录中寻找fixture文件。你可以设置FIXTURE\_DIRS选项为一个额外目录的列表，Django会从里面寻找。

运行manage.py loaddata命令的时候，你也可以指定一个fixture文件的目录，它会覆盖默认设置中的目录。

> 另见
>
> fixtrues也被用于测试框架来搭建一致性的测试环境。

### 提供初始SQL数据 <a href="#9b8cb8d0781de7ddc238a000dc6a2d54" id="9b8cb8d0781de7ddc238a000dc6a2d54"></a>

```
1.7中废除：

如果一个应用使用迁移，初始SQL数据将不会加载（包括后端特定的SQL数据）。由于Django 1.9中，迁移将会是必须的，这一行为经权衡后被废除。如果你想在应用中使用初始SQL数据，考虑在数据迁移中使用它们。
```

Django为数据库无关的SQL提供了一个钩子，当你运行migrate命令时，CREATE TABLE语句执行之后就会执行它。你可以使用这个钩子来建立默认的记录，或者创建SQL函数、视图、触发器以及其它。

钩子十分简单：Django会在你应用的目录中寻找叫做sql/\<modelname>.sql的文件，其中 \<modelname>是小写的模型名称。

所以如果在myapp应用中存在Person模型，你应该在myapp目录的文件sql/person.sql中添加数据库无关的SQL。下面的例子展示了文件可能会包含什么：

```
INSERT INTO myapp_person (first_name, last_name) VALUES ('John', 'Lennon');
INSERT INTO myapp_person (first_name, last_name) VALUES ('Paul', 'McCartney');
```

每个提供的SQL文件，都应该含有用于插入数据的有效的SQL语句（例如，格式适当的INSERT语句，用分号分隔）。

这些SQL文件可被manage.py中的 sqlcustom和sqlall命令阅读。详见manage.py文档。

注意如果你有很多SQL数据文件，他们执行的顺序是不确定的。唯一可以确定的是，在你的自定义数据文件被执行之前，所有数据表都被创建好了。

> 初始SQL数据和测试
>
> 这一技巧不能以测试目的用于提供初始数据。Django的测试框架在每次测试后都会刷新测试数据库的内容。所以，任何使用自定义SQL钩子添加的数据都会丢失。
>
> 如果你需要在测试用例中添加数据，你应该在测试fixture中添加它，或者在测试用例的setUp()中添加。

### 数据库后端特定的SQL数据 <a href="#7e3c8fe83ccf8673aa86d1b8812e4a74" id="7e3c8fe83ccf8673aa86d1b8812e4a74"></a>

没有钩子提供给后端特定的SQL数据。例如，你有分别为PostgreSQL和SQLite准备的初始数据文件。对于每个应用，Django都会寻找叫做\<app\_label>/sql/\<modelname>.\<backend>.sql的文件，其中\<app\_label>是小写的模型名称，\<modelname>是小写的模型名称，\<backend>是你的设置文件中由ENGINE提供的模块名称的最后一部分（例如，如果你定义了一个数据库，ENGINE的值为django.db.backends.sqlite3，Django会寻找\<app\_label>/sql/\<modelname>.sqlite3.sql）。

后端特定的SQL数据会先于后端无关的SQL数据执行。例如，如果你的应用包含了sql/person.sql 和sql/person.sqlite3.sql文件，而且你已经安装了SQLite应用，Django会首先执行 sql/person.sqlite3.sql的内容，其次才是sql/person.sql

[参考2](https://cloud.tencent.com/developer/article/1005694)
