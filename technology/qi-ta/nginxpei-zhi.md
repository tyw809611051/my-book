**nginx配置主要分为四部分：**main（全局设置）、events、http、server虚拟主机配置

**配置详解**
```
#nginx用户及组
user  www www;
#工作进程：数目，通常等于CPU数量或者2倍于CP
worker_processes auto;
#错误日志存放路径
error_log  /home/wwwlogs/nginx_error.log  crit;
#pid（进程标识符）：存放路径
pid        /usr/local/nginx/logs/nginx.pid;

#Specifies the value for maximum file descriptors that can be opened by this process.指定进程可以打开的最大描述符：数目。
worker_rlimit_nofile 51200;

events
    {
        #使用epoll的I/O 模型。linux建议epoll，FreeBSD建议采用kqueue，window下不指定
        use epoll;
        #每个工作进程的最大连接数
        worker_connections 51200;
        multi_accept on;
    }
```