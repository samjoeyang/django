# DjangoCMS工具栏配置

下面几个tags添加到模板中

`</head>`之前，引入css

```
{% render_block "css" %}
```

`<body>`后面第一行

```
{% cms_toolbar %}
```

`</body>`后面，引入js

```
{% render_block "js" %}
```

