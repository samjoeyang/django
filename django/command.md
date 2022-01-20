# 常用命令

一般情况下，Django的常用命令如下：

```
# 最常用，开发时，运行一个临时web服务，查看编码结果
python manage.py runserver 0.0.0.0:8000

# 收集静态文件
python manage.py collectstatic

python manage.py makemigrations [app]

python manage.py migrate [app]

# 导出数据
python manage.py dumpdata > db.json
#导出某一个应用的数据
python manage.py dumpdata app > app.json
# 导出某一个应用的某一张表的数据
python manage.py dumpdata app.table > table.json

# 导入数据，直接些json文件，不需要指定应用或表
python manage.py loaddata xxx.json

#安装依赖文件
pip install -r requirements.txt 

python manage.py cms check

#创建超级用户
python manage.py createsuperuser

python manage.py makemessages -l zh_Hans -i venv 
python manage.py compilemessages -i venv 

python manage.py syncdb # 已作废

# PYTHONIOENCODING=utf-8 
python test.py
```

可以通过`python manage.py --help`查看这些命令
