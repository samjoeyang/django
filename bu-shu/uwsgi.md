# uwsgi



*   安装

    ```python
    pip install uwsgi
    sudo apt-get install uwsgi-plugin-python3
    ```

    需要pcre支持`sudo apt-get install libpcre3 libpcre3-dev`
*   配置uwsgi.ini

    ```python
    [uwsgi]

    project=pyuno
    uid=root
    gid=root
    base=/var/www

    # python 虚拟环境路径: home 或 pyhome  或 virtualenv  或 venv 参数 指向 virtualenv 根目录
    # home=%(base)/%(project)/venv
    virtualenv=%(base)/%(project)/venv
    PYTHONPATH=%(base)/%(project)/venv

    # 工作路径
    chdir=%(base)/%(project)
    # django wsgi 路径
    wsgi-file=./%(project)/wsgi.py
    # module=%(project).wsgi:application
    master=True
    # 设置进程 processes 和 workers 一样的意思
    processes=2
    # workers = 2
    vacuum=True
    max-requests=5000
    # 每个进场下面的线程数
    threads=4

    # http=0.0.0.0:9090
    # 监听端口
    socket=0.0.0.0:9090
    # socket=uwsgi/pyuno.sock
    chown-socket=%(uid):www-data
    chmod-socket=664

    # uwsig pid 号
    pidfile=./uwsgi/%(project).pid
    # 日志文件
    daemonize=./uwsgi/%(project).log
    # 运行状态
    stats=./uwsgi/pyuno.stats
    # stats = 127.0.0.1:9191

    # 重启的时候使用的 pid 号
    touch-reload=%(base)/%(project)/uwsgi/%(project).pid

    #设置一个请求的超时时间(秒)，如果一个请求超过了这个时间，则请求被丢弃
    harakiri = 60
    #当一个请求被harakiri杀掉会，会输出一条日志
    harakiri-verbose = true
    # post 请求超过 字节 就缓存值磁盘
    post-buffering = 8192
    # 缓冲区大小
    buffer-size= 65535

    #开启内存使用情况报告
    memory-report = true

    #设置平滑的重启（直到处理完接收到的请求）的长等待时间(秒)
    reload-mercy = 10

    #设置工作进程使用虚拟内存超过N MB就回收重启
    reload-on-as= 1024
    # python 文件修改后自动重启
    python-autoreload=1

    # limit-as=500
    ```
* 启动uwsgi `uwsgin --ini uwsgi/uwsgi.ini`,可以加到`/etc/rc.local` 开机会自动启动`uwsgi`，在ini文件里设置 `py-auto-reload`代码修改后自动重启`uwsgi`，还可以用 `Supervisor`设置守护进程。
*   常用命令合集

    ```python
    # 启动uwsgi
    uwsgi --ini uwsgi/uwsgi.ini

    # 重启uwsgi
    uwsgi --reload uwsgi/pyuno.pid

    # 停止uwsgi
    uwsgi --stop uwsgi/pyuon.pid
    ```
* http 和 socket 区别 &#x20;
  * http:    add an http router/server on the specified address &#x20;
  * socket:  bind to the specified UNIX/TCP socket using default protocol
