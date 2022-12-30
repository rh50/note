
# linux资源限制

## 配置文件
    /etc/security/limits.conf

    soft nofile 655350  # 任何用户可以打开的最大的文件描述符数量，默认1024，这里的数值会限制tcp连接
    hard nofile 655350
    soft nproc  655350  # 任何用户可以打开的最大进程数
    hard nproc  650000
