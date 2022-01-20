# Redis与Cache

### **CACHES的配置**

本项目使用的redis进行的缓存 `sudo apt-get install -y redis` 配合hiredis访问redis

```bash
git clone https://github.com/redis/hiredis.git
cd hiredis & make & makeinstall
```

虚拟环境配合安装包

```bash
pip install django-redis
pip install django-redis-cache
pip install hiredis
```

`settings.py`里关于caches的配置如下：

```python
CACHES = {
    # "default":{
    #     "BACKEND": "django_redis.cache.RedisCache",
    #     "LOCATION": "127.0.0.1:6379",
    #     'OPTIONS': {
    #         #"CLIENT_CLASS": "redis_cache.client.DefaultClient",
    #         "DB": 0,
    #         "PARSER_CLASS": "redis.connection.HiredisParser",
    #         "CONNECTION_POOL_CLASS": "redis.BlockingConnectionPool",
    #         "PICKLE_VERSION": -1     
    #     }
    # },
    'default': {
        'BACKEND': 'redis_cache.RedisCache',
        'LOCATION': ['127.0.0.1:6379'],
        'OPTIONS': {
            'DB': 1,
            'PARSER_CLASS': 'redis.connection.HiredisParser',
            'CONNECTION_POOL_CLASS': 'redis.BlockingConnectionPool',
            'CONNECTION_POOL_CLASS_KWARGS': {
                'max_connections': 50,
                'timeout': 20,
            },
            'MAX_CONNECTIONS': 1000,
            'PICKLE_VERSION': -1,
        },
    },
    # 存放微信公众号 token
    'wechat': {
        'BACKEND': 'redis_cache.RedisCache',
        'LOCATION': ['127.0.0.1:6379'],
        'OPTIONS': {
            'DB': 2,
            'PARSER_CLASS': 'redis.connection.HiredisParser',
            'CONNECTION_POOL_CLASS': 'redis.BlockingConnectionPool',
            'CONNECTION_POOL_CLASS_KWARGS': {
                'max_connections': 50,
                'timeout': 20,
            },
            'MAX_CONNECTIONS': 1000,
            'PICKLE_VERSION': -1,
        },
    }
}
```

### ****
