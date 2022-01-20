# 安装



1. 执行以下命令安装django CMS installer\
   `pip install djangocms-installer`
2. 建立项目目录\
   执行mkdir命令，建立djangocms目录，执行cd命令进入这个目录。\
   `mkdir unoecp && cd unoecp`
3. 建立一个项目 执行以下命令，建立一个名为unoecp的新的django项目,这个命令的意思是运行django CMS installer，“-f”表示同时安装Django Filer(Django Filer是一个用来管理文件和处理图片的组件，几乎所有的django CMS项目都用到它。)，“-p .”表示使用当前目录作为新项目的目录，“-s“ 表示跳过检查。\
   `djangocms -s -f -p . unoecp`\
   执行上面的命令之后，会出现一个`please wait while install dependencies`的提示，并且会停留一段时间，此时等待即可。
4.  数据库建表

    ```python
    python manage.py makemigrations
    python mamage.py migrate
    ```
5. 启动服务，可指定端口\
   `python manage.py runserver 0.0.0.0:8000`
6. 检测是否安装成功 打开浏览器，输入`http://localhost:8000/` 如果正常浏览就表示DjangoCMS安装成功了。
7. 登陆后台 输入用户名：admin，密码：admin，进行登陆。

> 手动创建root用户,命令行里输入\
> `python manage.py createsuperuser`\
> 按照提示步骤输入用户名（默认root）、密码、邮箱地址，然后在运行服务\
> `python manage.py runserver 8000`
