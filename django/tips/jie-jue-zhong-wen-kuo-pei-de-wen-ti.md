# 中文适配的问题

Python2有UTF-8的问题，可以在文件开头首行加入`# -*- coding: UTF-8 -*-`即可 在项目的settings.py文件中加入

```
import sys
reload(sys)
sys.setdefaultencoding('utf-8')
```
