---
description: 本章节包含了DjangoCMS的国际化设置，所以放在了这里，其主要部分还只是Django的国际化
---

# Django的国际化

在Django框架下，国际化不需要另外安装package，只需要在`settings.py`文件中进行配置，在配置前系统需要安装`gettext`,例如`Ubuntu`系统需要运行 `sudo apt-get install gettext`

1.  开启

    ```python
    from django.utils.translation import ugettext_lazy as _

    MIDDLEWARE_CLASSES =(
       ...
       'dngo.middleware.locale.LocaleMiddleware',
    )

    LANGUAGE_CODE ='zh-hans'
    TIME_ZONE ='UTC'
    USE_I18N =True
    USE_L10N =True
    USE_TZ =True

    LANGUAGES =(
        ('zh-hans', _('Simplified Chinese')),
        ('zh', _('zh')),
        ('en', gettext('en')),
        ('zh-Hant',_('中文繁體')),
    )

    #翻译文件所在目录，需要手工创建
    LOCALE_PATHS =(
       os.path.join(BASE_DIR, 'locale'),
    )

    TEMPLATE_CONTEXT_PROCESSORS =(
       ...
       "django.core.context_processors.i18n",
    )
    ```
2.  DjangoCMS有关国际化的配置如下(包含Aldryn\_newsblog的语言配置)：

    ```python
    CMS_LANGUAGES = {
        ## Customize this
        1: [
            {
                'code': 'zh-hans',
                'name': _('Simplified Chinese'),
                'redirect_on_fallback': False,
                'public': True,
                'hide_untranslated': False,
                # 'fallbacks': ['zh','en','de', 'fr', 'nl'],
            },
            {
                'code': 'zh',
                'name': _('zh'),
                'redirect_on_fallback': True,
                'public': True,
                'hide_untranslated': True,
                'fallbacks': ['zh-hans'],
            },
            {
                'code': 'en',
                'name': gettext('English'),
                'redirect_on_fallback': True,
                'public': False,
                'hide_untranslated': True,
                'fallbacks': ['zh-hans','zh'],
            },
        ],
        2: [ # 这部分可以省略
            {
                'code': 'de',
                'name': 'CMS:' + gettext('Deutsch'),
                'redirect_on_fallback': True,
                'public': True,
                'hide_untranslated': True,
                'fallbacks': ['zh-hans', 'en'],
            },
            {
                'code': 'fr',
                'name': 'CMS:' + gettext('French'),
                'redirect_on_fallback': True,
                'public': True,
                'hide_untranslated': True,
                'fallbacks': ['zh-hans', 'en'],
            },
        ],
        'default': {
            'redirect_on_fallback': True,
            'public': True,
            'hide_untranslated': True,
            'fallbacks': ['zh-hans'],
            # 'code': 'zh-hans',
            # 'name': gettext('Chinese'),
        },
    }

    # for aldryn_newsblog
    PARLER_LANGUAGES = {
        None:(
            {'code': 'zh-hans'},
            {'code': 'zh'},
            {'code': 'en'},
        ),
        'default':{
            'fallback':'zh-hans',
            'hide_untranslated':True,
        }
    }

    PARLER_DEFAULT_LANGUAGE_CODE = 'zh-hans'
    ```
3.  生成需要翻译的文件 &#x20;

    `python manage.py makemessages -l zh_Hans -i venv`    \
    &#x20;

    > 注意：此处`zh_Hans`里的H是大写，`-i`的意义是忽略`venv`目录
    >
    > 注2：`zh-Hans`大写是在Django-1.11版本，在3.1版本时，已经忽略大小写了
4. 手工翻译 `locale` 目录中的 django.po &#x20;
5.  翻译完成后需要运行编译 &#x20;

    `python manage.py compilemessages`
6.  在`urls.py`中关于国际的的设置：  (这个设置的做用有点忘记了，有时候可以不设置）

    ```
    urlpatterns = [
        ...
        path("i18n/", include("django.conf.urls.i18n")),
        ...
    ]
    urlpatterns += i18n_patterns(
        ...
    )
    ```
7. 刷新页面查看翻译结果

###
