# MySQL-Server安装

## 安装

```bash
# 安装
sudo apt-get install mysql-server

# 启动
service mysql start

# 查看初始用户名密码
cat /etc/mysql/debian.cnf | grep user | head -n 1

cat /etc/mysql/debian.cnf | grep password | head -n 1

# 登录mysql
mysql -udebian-sys-maint -p
```

```bash
# 修改root密码
alter user 'root'@'localhost' identified by '新密码';

# 创建新的database
CREATE DATABASE IF NOT EXISTS yourdbname DEFAULT CHARSET utf8 COLLATE utf8_general_ci;

# 创建新的用户
create user 'pyuno'@'localhost' identified by '新密码';

# 新用户赋权
GRANT ALL PRIVILEGES ON pyuno.* to "pyuno"@"localhost" IDENTIFIED BY "新密码";
FLUSH PRIVILEGES;

# 退出mysql
quit

# 重启

service mysql restart
```

## mysqlclient插件安装

#### Django1.11时需要安装以下两个，这次升级到Django3.1后，只需要安装`mysqlcliet`

```python
pip install PyMySQL
pip install mysqlclient
```

注：mysqlclient的某些版本会安装时报错，Django1.11时对应可安装可使用的mysqlclient==1.4.2.post1，Django3.1对应可安装可使用的版本mysqlclient>=2.0

Django 1.11时需要修改项目目录下的`__init__.py`文件，Django3.1不需要

```python
import pymysql
pymysql.install_as_MySQLdb()

SITE_DIR = os.path.join(BASE_DIR,"sites")
sys.path.append(SITE_DIR)
```

####

```bash
# sudo apt-get install python3-dev default-libmysqlclient-dev libmysqlclient-dev
sudo apt-get install python3-dev default-libmysqlclient-dev build-essential
pip install mysqlclient
pip install PyMySQL # Django 3.1 不需要安装这个package
```

