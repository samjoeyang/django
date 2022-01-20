---
description: django-allauth
---

# 用户系统

使用django-allauth(0.39.1)

1.  安装 &#x20;

    `pip install django-allauth`
2.  配置\
    settings.py (Important - Please note ‘django.contrib.sites’ is required as INSTALLED\_APPS):

    \`\`\`python

    **Specify the context processors as follows:**

    TEMPLATES = \[ { 'BACKEND': 'django.template.backends.django.DjangoTemplates', 'DIRS': \[], 'APP\_DIRS': True, 'OPTIONS': { 'context\_processors': \[

    ```
             # Already defined Django-related contexts here

             # `allauth` needs this from django
             'django.template.context_processors.request',
         ],
     },
    ```

    }, ]

AUTHENTICATION\_BACKENDS = ( ...

```
# Needed to login by username in Django admin, regardless of `allauth`
'django.contrib.auth.backends.ModelBackend',

# `allauth` specific authentication methods, such as login by e-mail
'allauth.account.auth_backends.AuthenticationBackend',
...
```

)

INSTALLED\_APPS = ( ...

```
# The following apps are required:
'django.contrib.auth',
'django.contrib.messages',
'django.contrib.sites',

'allauth',
'allauth.account',
'allauth.socialaccount',
# ... include the providers you want to enable:
'allauth.socialaccount.providers.agave',
'allauth.socialaccount.providers.amazon',
'allauth.socialaccount.providers.angellist',
'allauth.socialaccount.providers.asana',
'allauth.socialaccount.providers.auth0',
'allauth.socialaccount.providers.authentiq',
'allauth.socialaccount.providers.baidu',
'allauth.socialaccount.providers.basecamp',
'allauth.socialaccount.providers.bitbucket',
'allauth.socialaccount.providers.bitbucket_oauth2',
'allauth.socialaccount.providers.bitly',
'allauth.socialaccount.providers.cern',
'allauth.socialaccount.providers.coinbase',
'allauth.socialaccount.providers.dataporten',
'allauth.socialaccount.providers.daum',
'allauth.socialaccount.providers.digitalocean',
'allauth.socialaccount.providers.discord',
'allauth.socialaccount.providers.disqus',
'allauth.socialaccount.providers.douban',
'allauth.socialaccount.providers.draugiem',
'allauth.socialaccount.providers.dropbox',
'allauth.socialaccount.providers.dwolla',
'allauth.socialaccount.providers.edmodo',
'allauth.socialaccount.providers.eveonline',
'allauth.socialaccount.providers.evernote',
'allauth.socialaccount.providers.facebook',
'allauth.socialaccount.providers.feedly',
'allauth.socialaccount.providers.fivehundredpx',
'allauth.socialaccount.providers.flickr',
'allauth.socialaccount.providers.foursquare',
'allauth.socialaccount.providers.fxa',
'allauth.socialaccount.providers.github',
'allauth.socialaccount.providers.gitlab',
'allauth.socialaccount.providers.google',
'allauth.socialaccount.providers.hubic',
'allauth.socialaccount.providers.instagram',
'allauth.socialaccount.providers.jupyterhub',
'allauth.socialaccount.providers.kakao',
'allauth.socialaccount.providers.line',
'allauth.socialaccount.providers.linkedin',
'allauth.socialaccount.providers.linkedin_oauth2',
'allauth.socialaccount.providers.mailru',
'allauth.socialaccount.providers.mailchimp',
'allauth.socialaccount.providers.meetup',
'allauth.socialaccount.providers.microsoft',
'allauth.socialaccount.providers.naver',
'allauth.socialaccount.providers.nextcloud',
'allauth.socialaccount.providers.odnoklassniki',
'allauth.socialaccount.providers.openid',
'allauth.socialaccount.providers.orcid',
'allauth.socialaccount.providers.paypal',
'allauth.socialaccount.providers.patreon',
'allauth.socialaccount.providers.persona',
'allauth.socialaccount.providers.pinterest',
'allauth.socialaccount.providers.reddit',
'allauth.socialaccount.providers.robinhood',
'allauth.socialaccount.providers.sharefile',
'allauth.socialaccount.providers.shopify',
'allauth.socialaccount.providers.slack',
'allauth.socialaccount.providers.soundcloud',
'allauth.socialaccount.providers.spotify',
'allauth.socialaccount.providers.stackexchange',
'allauth.socialaccount.providers.steam',
'allauth.socialaccount.providers.stripe',
'allauth.socialaccount.providers.trello',
'allauth.socialaccount.providers.tumblr',
'allauth.socialaccount.providers.twentythreeandme',
'allauth.socialaccount.providers.twitch',
'allauth.socialaccount.providers.twitter',
'allauth.socialaccount.providers.untappd',
'allauth.socialaccount.providers.vimeo',
'allauth.socialaccount.providers.vimeo_oauth2',
'allauth.socialaccount.providers.vk',
'allauth.socialaccount.providers.weibo',
'allauth.socialaccount.providers.weixin',
'allauth.socialaccount.providers.windowslive',
'allauth.socialaccount.providers.xing',
...
```

)

SITE\_ID = 1

**############**

## allauth基本设定 \#

**############**

ACCOUNT\_AUTHENTICATION\_METHOD = 'username\_email' ACCOUNT\_EMAIL\_REQUIRED = True LOGIN\_REDIRECT\_URL = "/case"

## ACCOUNT\_SIGNUP\_FORM\_CLASS = 'users.forms.registions'

AUTHENTICATION\_BACKENDS = ( 'allauth.account.auth\_backends.AuthenticationBackend', 'django.contrib.auth.backends.ModelBackend', )

**####################**

## django-auth登录地址设定  \#

**####################**

LOGIN\_URL="/users/login/" #?next=/

**######**

## 邮箱设定  \#

**######**

EMAIL\_HOST = "smtp.mail.com" EMAIL\_PORT = 25 #QQ邮箱使用587 EMAIL\_HOST\_USER = "user@mail.com" EMAIL\_HOST\_PASSWORD = "password" # 这个不是邮箱密码，而是授权码 EMAIL\_USE\_TLS = True # 这里必须是 True，否则发送不成功 EMAIL\_FROM = "user@mail.com" # 发件人 DEFAULT\_FROM\_EMAIL = "UNOECP [user@mail.com](mailto:user@mail.com)" # 默认发件人(如果不添加DEFAULT\_FROM\_EMAIL字段可能会导致如下错误: 451, b'Sender address format error.', 'webmaster@localhost')

````
urls.py:  
```python 
urlpatterns = [
    ...
    url(r'^accounts/', include('allauth.urls')),
    ...
]
````

1.  数据库 &#x20;

    `python manage.py migrate` &#x20;
2.  allath没有用户资料修改功能，需要自己编写，可以扩展用户资料，相关问题想看代码本部分，在url中的配置参考以下 &#x20;

    ```python
    url(r'^accounts/', include('allauth.urls')),
    url(r'^accounts/profile/', include('users.urls')),
    ```

### ****

##
