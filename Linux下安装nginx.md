# Linux下安装nginx

## 进入home目录创建目录 nginx

## 准备nginx安装相关的组件

### 下载nginx: `wget http://nginx.org/download/nginx-1.10.2.tar.gz`

### 下载openssl: `wget http://www.openssl.org/source/openssl-fips-2.0.10.tar.gz`

### 下载zlib: `wget http://zlib.net/zlib-1.2.11.tar.gz`

### 下载pcre: `wget https://netix.dl.sourceforge.net/project/pcre/pcre/8.40/pcre-8.40.tar.gz`

### 如果安装了c++的环境就可跳过，如未安装：yum install gcc-c++ （点击y即可）

>安装结尾显示complete,即代表安装完成

## 以上文件准备好开始安装

### 安装openssl

```shell
tar -zxvf openssl-fips-2.0.10.tar.gz

cd openssl-fips-2.0.10

./config && make && make install
```

### 安装pcre

```shell
tar -zxvf pcre-8.40.tar.gz

cd pcre-8.40

./configure && make && make install
```

### 安装zlib

```shell
tar -zxvf zlib-1.2.11.tar.gz

cd zlib-1.2.11

./configure && make && make install
```

### 安装nginx

```shell
tar zxvf nginx-1.10.2.tar.gz

cd nginx-1.10.2

./configure && make && make install
```

### 启动nginx

> 查看nginx安装的地址（`whereis nginx`）

```shell
# 进入目录
cd /usr/local/nginx/
# 启动nginx
/usr/local/nginx/sbin/nginx
# 查看启动状态
ps  -ef | grep nginx
```

### 检查防火墙状态

```shell
# 防火墙状态
firewall-cmd --stat
# 如果防火墙为开启 则启动防火墙
systemctl start firewalld
```

### 添加端口

```shell
# 添加80端口 --permanent永久生效，没有此参数重启后失效
firewall-cmd --zone=public --add-port=80/tcp --permanent
# 添加3306端口 mysql
firewall-cmd --zone=public --add-port=3306/tcp --permanent
# 添加8686端口 自己项目的端口
firewall-cmd --zone=public --add-port=8686/tcp --permanent
# 重启防火墙
firewall-cmd --reload
# 查看添加的端口
firewall-cmd --list-ports
```

### ngxin配置

> 配置文件地址 `cd /usr/local/nginx/conf`

#### nginx.conf

```conf
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

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        # 端口号
        listen       80;
        # 访问域名
        server_name  www.域名.com;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            # 服务器地址：端口号
            proxy_pass   http://0.0.0.0:0000;
            root   html;
            index  MP_verify_NqHE4ElE6bsy5ZpL.txt;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ {
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht {
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server {
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}


    # HTTPS server
    #
    #server {
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}
```

### 重新加载配置文件

`nginx -s reload`
