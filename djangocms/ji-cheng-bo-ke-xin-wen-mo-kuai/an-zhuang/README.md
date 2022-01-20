# 安装







1.  安装Aldryn News & Blog 进入我们的项目所在的开发环境，执行命令安装,环境不同安装目录有所不同，请注意\
    `pip install aldryn-newsblog`

    > 注：此处多次没有安装成功，主要原因是在安装依赖`aldryn-apphooks-config`时遇到acsi码的问题，python3.6已经默认支持utf-8,而不知道什么原因安装包里的`README.srt`文件读取时遇到编码问题，把安装包下载下来之后，笔者把安装包里的`setup.py`文件中读取`README.srt`的行注释掉了，使用`python setup.py install`手动安装了这个依赖包,再重新运行`pip install aldryn-newsblog`，安装成功
2.  配置Aldryn News & Blog\
    打开项目的`settings.py`文件，将以下代码加入到`INSTALLED_APPS`的`'cms'`后面

    ```python
    # you will probably need to add these
    'aldryn_apphooks_config',
    'aldryn_categories',
    'aldryn_common',
    'aldryn_newsblog',
    'aldryn_people',
    'aldryn_translation_tools',
    'parler',
    'sortedm2m',
    'taggit',
    ```

    ```python
    # you'll almost certainly have these installed already
    'djangocms_text_ckeditor',
    'easy_thumbnails',
    'filer',
    ```
3.  执行命令，进行数据库同步。 &#x20;

    `python manage.py migrate`
