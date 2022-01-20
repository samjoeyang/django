# 小问题

在Python3的环境下，可能报·`python_2_unicode_compatible`·错误

需要将代码替换以下

```
from django.utils.encoding import python_2_unicode_compatible
```

```
from six import python_2_unicode_compatible
```

也运行以下代码即可

```
#!/bin/sh
sed -i 's#from django.utils.encoding import python_2_unicode_compatible#from six import python_2_unicode_compatible#' /usr/local/lib/python3.7/site-packages/aldryn_categories/models.py &&
sed -i 's#from django.utils.encoding import force_text, python_2_unicode_compatible#from django.utils.encoding import force_text#' /usr/local/lib/python3.7/site-packages/aldryn_newsblog/models.py &&
sed -i '/from django.utils.encoding import force_text/afrom six import python_2_unicode_compatible' /usr/local/lib/python3.7/site-packages/aldryn_newsblog/models.py &&
sed -i 's#from six import python_2_unicode_compatible/#from six import python_2_unicode_compatible#' /usr/local/lib/python3.7/site-packages/aldryn_newsblog/models.py &&
sed -i 's#from django.utils.encoding import force_text, python_2_unicode_compatible#from django.utils.encoding import force_text#' /usr/local/lib/python3.7/site-packages/aldryn_people/models.py &&
sed -i '/from django.utils.encoding import force_text/afrom six import python_2_unicode_compatible' /usr/local/lib/python3.7/site-packages/aldryn_people/models.py &&
sed -i 's#from django.utils.encoding import python_2_unicode_compatible#from six import python_2_unicode_compatible#' /usr/local/lib/python3.7/site-packages/aldryn_newsblog/cms_appconfig.py
```
