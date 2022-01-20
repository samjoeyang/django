# Django调试工具debug\_toolbar

### django 调试工具debug\_toolbar

1. 安装: `pip install django-debug-toolbar` &#x20;
2. 添加配置内容到项目settings.py文件: &#x20;
   * 注册apps:  `'debug_toolbar'`, &#x20;
   * 添加中间键: `'debug_toolbar.middleware.DebugToolbarMiddleware'`, &#x20;
   * `DEBUG_TOOLBAR_PATCH_SETTINGS = False` #不修改默认配置
   * `INTERNAL_IPS = ('127.0.0.1',)` # 监听ip &#x20;
   *   \`DEBUG\_TOOLBAR\_CONFIG = { &#x20;

       &#x20;'SHOW\_TOOLBAR\_CALLBACK': 'ddt\_request\_history.panels.request\_history.allow\_ajax', &#x20;

       }\`
   * `DEBUG_TOOLBAR_CONFIG={'JQUERY_URL': r"http://code.jquery.com/jquery-2.1.1.min.js"}`
3.  修改项目urls.py:

    ```python
    from django.conf.urls import url

    if settings.DEBUG:  
     import debug_toolbar
     urlpatterns = [url(r'^__debug__/', include(debug_toolbar.urls)), ] + urlpatterns
    ```
4. 启动项目即可在页面看到效果，页面风格可以选择，
   * site-packages --->django\_debug\_toolbar----->settings.py
   * 打开settings文件后找得到(CONFIG\_DEFAULTS) 变量 ， 修改key: JQUERY\_URL的value。
   *   第三方面板:

       ```python
       # 查看您的Haystack后端所做的查询 
       haystack_panel.panel.HaystackDebugPanel 
       #  验证您的HTML并显示警告和错误 
       debug_toolbar_htmltidy.panels.HTMLTidyDebugPanel 
       #  使用调试语句检索并显示您指定的信息。Inspector面板也会默认登录到控制台 
       inspector_panel.panels.inspector.InspectorPanel 
       #  提供了一个profiling panel，它包含了line_profiler的输出 
       debug_toolbar_line_profiler.panel.ProfilingPanel 
       #  跟踪memcached的使用情况。它目前支持pylibmc和memcache库 
       memcache_toolbar.panels.memcache.MemcachePanel或memcache_toolbar.panels.pylibmc.PylibmcPanel 
       #  添加MongoDB调试信息 
       debug_toolbar_mongo.panel.MongoDebugPanel 
       #  在你的django应用程序中跟踪neo4j rest API调用，这也适用于
       neo4django和neo4jrestclient neo4j_panel.Neo4jPanel 
       #  浏览在django.contrib.sites中注册的网站并在它们之间切换。用于调试使用动态设置的SITE_ID的django-dynamicsites项目。
       sites_toolbar.panels.SitesDebugPanel 
       #  显示您的Django应用程序的模板渲染时间 
       template_timings_panel.panels.TemplateTimings.TemplateTimings 
       #  轻松切换登录用户，查看当前用户的属性 
       debug_toolbar_user_panel.panels.UserPanel
       ```

###
