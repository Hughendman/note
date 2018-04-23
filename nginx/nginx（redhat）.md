```
1      安装依赖包
模块依赖性Nginx需要依赖下面3个包

1.        gzip 模块需要 zlib 库 ( 下载:http://www.zlib.net/ )

2.        rewrite 模块需要 pcre 库 ( 下载:http://www.pcre.org/ )

3.        openssl库需要perl （下载：https://www.perl.org）

4.        ssl 功能需要 openssl 库 ( 下载:http://www.openssl.org/ )

1.1  zlib库
安装步骤：

1.   下载安装包：

wget http://www.zlib.net/zlib-1.2.8.tar.gz

2.   解压安装包：

tar –zxvf zlib-1.2.8.tar.gz

3.   执行安装：

./configure&& make && make install

1.2  pcre库
安装步骤：

1.   下载安装包：

wget https://www.openssl.org/source/openssl-1.1.0c.tar.gz

2.   解压安装包：

tar –zxvf openssl-1.1.0c.tar.gz

3.   执行安装：

./configure &&make && make install

1.3  perl库
安装步骤：

1.   下载安装包：

wget http://www.cpan.org/src/5.0/perl-5.24.0.tar.gz

2.   解压安装包：

tar –zxvf perl-5.24.0.tar.gz

3.   执行安装：

./Configure&& make && make install

安装过程比较长，按照提示内容，一直下一步就行。

1.4  openssl库
安装步骤：

1.   下载安装包：

wget https://www.openssl.org/source/openssl-1.1.0c.tar.gz

2.   解压安装包：

tar –xvf openssl-1.1.0c.tar.gz

3.   执行安装：

./config && make && make install

安装过程较长，一直等待就行

2      安装nginx
1.      下载安装包：

wget http://nginx.org/download/nginx-1.9.9.tar.gz

2.      解压安装包：

tar –zxvf nginx-1.9.9.tar.gz

3.      执行安装：

./configure--with-pcre=../pcre-8.38 --with-zlib=../zlib-1.2.8 --with-openssl=../openssl-1.1.0c

make &&make install

3      配置启动服务
步骤如下：

1.      输入命令：cd /etc/init.d/

2.      创建nginx文件：vi nginx

3.      复制以下内容：

#!/bin/bash 

# nginxStartup script for the Nginx HTTP Server 

# 

#chkconfig: - 85 15 

#description: Nginx is a high-performance web and proxy server. 

# It hasa lot of features, but it's not for everyone. 

#processname: nginx 

#pidfile: /var/run/nginx.pid 

# config:/usr/local/nginx/conf/nginx.conf 

nginxd=/usr/local/nginx/sbin/nginx 

nginx_config=/usr/local/nginx/conf/nginx.conf 

nginx_pid=/usr/local/nginx/nginx.pid 

 

RETVAL=0 

prog="nginx"

 

# Sourcefunction library. 

./etc/rc.d/init.d/functions 

 

# Sourcenetworking configuration. 

./etc/sysconfig/network 

 

# Checkthat networking is up. 

[${NETWORKING} = "no" ] && exit 0 

 

[ -x$nginxd ] || exit 0 

 

 

# Startnginx daemons functions. 

start(){ 

 

if [ -e$nginx_pid ];then

   echo "nginx already running...."

   exit 1 

fi 

 

   echo -n $"Starting $prog: "

   daemon $nginxd -c ${nginx_config} 

   RETVAL=$? 

   echo 

   [ $RETVAL = 0 ] && touch/var/lock/subsys/nginx 

   return $RETVAL 

 

} 

 

 

# Stopnginx daemons functions. 

stop(){ 

        echo -n $"Stopping $prog: "

        killproc $nginxd 

        RETVAL=$? 

        echo 

        [$RETVAL = 0 ] && rm -f /var/lock/subsys/nginx /var/run/nginx.pid 

} 

 

 

# reloadnginx service functions. 

reload(){ 

 

    echo -n $"Reloading $prog: "

 $nginxd -s reload 

    #if your nginx version is below 0.8, pleaseuse this command: "kill -HUP `cat ${nginx_pid}`"

    RETVAL=$? 

    echo 

 

} 

 

# See howwe were called. 

case"$1" in

start) 

        start 

        ;; 

 

stop) 

        stop 

        ;; 

 

reload) 

        reload 

        ;; 

 

restart) 

        stop 

        start 

        ;; 

 

status) 

        status $prog 

        RETVAL=$? 

        ;; 

*) 

        echo $"Usage: $prog{start|stop|restart|reload|status|help}"

        exit 1 

esac 

 

exit $RETVAL

4.      启动nginx：service nginx start
```