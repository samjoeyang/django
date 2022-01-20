# settings配置



1. 修改`ALLOWED_HOSTS = []`替换为`ALLOWED_HOSTS = ['*']` &#x20;
2. 修改`TIME_ZONE = 'Etc/UTC'`替换为`TIME_ZONE = 'Asia/Shanghai'` &#x20;
3. 设置`SITE_ID=1`,必须有 &#x20;
4.  添加  （Django3.1不需要）

    ```python
     import sys  
     sys.path.append('/var/www/djangocms/env/lib/python2.7/site-packages/')
    ```
5. LANGUAGE\_CODE设置可根据自己需要进行修改，本项目安装完即`LANGUAGE_CODE = 'zh-hans'` &#x20;
6.  设置DATABASE &#x20;

    ```python
     'default': {
             'ENGINE': 'django.db.backends.mysql',
             'NAME': 'db_name',
             'USER': 'username',
             'PASSWORD': 'password',
             'HOST': 'host ip or domain',
             'PORT': '3306',
             }
     }
    ```
7.  在app目录下的`__init__.py`加入（Django-3.1不需要此操作，安装mysqlclient>=2.0即可）

    ```python
     import pymysql
     pymysql.install_as_MySQLdb()

     SITE_DIR = os.path.join(BASE_DIR,"sites")
     sys.path.append(SITE_DIR)
    ```

### ****
