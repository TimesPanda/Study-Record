#### 1、配置Nginx服务器
```
#user  nobody;
worker_processes  1;
#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;
#pid        logs/nginx.pid;
events {
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    #tcp_nopush     on;
    #keepalive_timeout  0;
    keepalive_timeout  65;
    #gzip  on;
    upstream  localhost   {  
	  server   localhost:8080 weight=1;  
	  server   localhost:9091 weight=2;  
	  server   localhost:9092 weight=3; 
    }
    server {
        listen       9999;
        server_name  localhost;
        #charset koi8-r;
        #access_log  logs/host.access.log  main;
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
	location / { 
		root   html; 
		index  index.html index.htm; 
		proxy_pass        http://localhost;  
		proxy_set_header  X-Real-IP  $remote_addr;  
		client_max_body_size  100m;  
	} 
   }
}
```

#### 2、配置Redis
在redis配置文件中开启几个选项即可
```
找到# requirepass foobared ，修改为  requirepass 123456 
123456为redis密码 
appendonly yes #启用aof 持久化方式 
# appendfsync always //收到写命令就立即写入磁盘,最慢,但是保证完全的持久化 
appendfsync everysec //每秒钟写入磁盘一次,在性能和持久化方面做了很好的折中 
# appendfsync no //完全依赖os,性能最好,持久化没保证 
# rename-command CONFIG b840fc02d524045429941cc15f59e41cb7be6c52  ###重定义命令，例如将CONFIG命令更名为一个很复杂的名字：  
# rename-command CONFIG ""  取消这个命令； 
```

#### 3、配置Tomcat内容:context.xml
```
<?xml version='1.0' encoding='utf-8'?>
<Context>
    <!-- Default set of monitored resources -->
    <WatchedResource>WEB-INF/web.xml</WatchedResource>
	<!-- 单点配置 -->
	<!-- 原始的：com.radiadesign.catalina.session.RedisSessionHandlerValve com\bluejeans\tomcat\redissessions  -->
	<Valve className="com.bluejeans.tomcat.redissessions.RedisSessionHandlerValve"/>
	<Manager className="com.bluejeans.tomcat.redissessions.RedisSessionManager"
	host="10.0.81.212"
	port="6379"
	password="123456"
	database="0"
	maxInactiveInterval="60"/>

</Context>
```

##### 4、启动相关注意事项
```
运行cmd
然后到redis路径
运行命令: redis-server redis.windows.conf
```
```
1、启动：
C:\server\nginx-1.0.2>start nginx
或
C:\server\nginx-1.0.2>nginx.exe
注：建议使用第一种，第二种会使你的cmd窗口一直处于执行中，不能进行其他命令操作。

2、停止：
C:\server\nginx-1.0.2>nginx.exe -s stop
或
C:\server\nginx-1.0.2>nginx.exe -s quit
注：stop是快速停止nginx，可能并不保存相关信息；quit是完整有序的停止nginx，并保存相关信息。
```
```
1字节的UTF-8序列的字节1无效
1.手动将<?xml version="1.0" encoding="UTF-8"?>中的UTF-8更改成UTF8
2.使用记事本打开该xml文件,另存为时候编码格式选择UTF-8.
```
