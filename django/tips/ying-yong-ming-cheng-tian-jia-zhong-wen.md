# 应用名称如何使用中文

通过修改应用目录下`__init__.py`文件，代码中`app.AppConfig`中的`app`和`AppConfig`是可以根据项目情况自己定义

```
# -*- coding: UTF-8 -*-
import os
from django.apps import AppConfig

default_app_config="app.AppConfig"

def get_current_app_name(_file):
    return os.path.split(os.path.dirname(_file))[-1]

class AppConfig(AppConfig):
  name = get_current_app_name(__file__)
  verbose_name = u'应用名称'
```
