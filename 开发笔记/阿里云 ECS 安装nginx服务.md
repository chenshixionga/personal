### 1、注册阿里云账号，或者用其他账号登录

### 2、实例化ECS  选择系统linux

### 3、安装nginx 
   #### 1.添加资源

   添加CentOS 7 Nginx yum资源库,打开终端,使用以下命令(没有换行):
   ```
     sudo rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
   ```

   #### 2.安装Nginx

   在你的CentOS 7 服务器中使用yum命令从Nginx源服务器中获取来安装Nginx：

   这里有一个需要注意的地方，尽量不要用网上的下载源码包然后再传到服务器上的方式进行安装，因为nginx已经不算是简单的Linux了，做了很多扩展，这个时候如     果你用源码包安装会出现各种各样的问题，尽量用已经封装好的rpm\yum进行安装
   ```
   sudo yum install -y nginx
   ```
   Nginx将完成安装在你的CentOS 7 服务器中。

   #### 3.启动Nginx

   刚安装的Nginx不会自行启动。运行Nginx:
   ```
   sudo systemctl start nginx.service
   ```
   如果一切进展顺利的话，现在你可以通过你的域名或IP来访问你的Web页面来预览一下Nginx的默认页面
   
   
### 4.完全卸载掉nginx
```
  rm -rf /etc/nginx/
  rm -rf /usr/sbin/nginx
  rm /usr/share/man/man1/nginx.1.gz
  apt-get remove nginx*
```
```
  rm -rf /etc/nginx/
  rm -rf /usr/sbin/nginx
  rm /usr/share/man/man1/nginx.1.gz
  yum remove nginx*
```
### 5.配置命令操作
   ① 打开文件  /etc/nginx/nginx.conf 
   ```
      vim /etc/nginx/nginx.conf  
   ```
   ② 进入编辑状态 i
   ```
     i
   ```
   ③ 退出编辑状态 esc 键
   ```
     ESC
   ```
   ④ 保存并退出文件 
   ```
     :wq
   ```
   
   
   1.使用xshell登录到阿里云服务器。安装nginx（本文安装到/etc下）

[plain] view plain copy
cd /etc  
apt-get update  
apt-get install nginx  
2.首先先配置nginx，然后再根据配置文件做下一步操作

打开/etc/nginx/nginx.conf文件

[plain] view plain copy
vim /etc/nginx/nginx.conf  
在nginx.conf中配置如下：
[plain] view plain copy
user www-data;  
worker_processes auto;  
pid /run/nginx.pid;  
events {  
        worker_connections 768;  
        # multi_accept on;  
}  
http {  
  
        ##  
        # Basic Settings  
        ##  
  
        tcp_nodelay on;  
        keepalive_timeout 65;  
        types_hash_max_size 2048;  
        # server_tokens off;  
  
        # server_names_hash_bucket_size 64;  
        # server_name_in_redirect off;  
  
        include /etc/nginx/mime.types;  
        default_type application/octet-stream;  
  
        ##  
        # SSL Settings  
        ##  
  
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Dropping SSLv3, ref: POODLE  
        ssl_prefer_server_ciphers on;  
  
        ##  
        # Logging Settings  
        ##  
  
        access_log /var/log/nginx/access.log;  
        error_log /var/log/nginx/error.log;  
  
        ##  
        # Gzip Settings  
        ##  
  
        gzip on;  
        gzip_disable "msie6";  
  
        # gzip_vary on;  
        # gzip_proxied any;  
        # gzip_comp_level 6;  
        # gzip_buffers 16 8k;  
        # gzip_http_version 1.1;  
  
        ##  
        # Virtual Host Configs  
        ##  
  
  
        gzip on;  
        gzip_disable "msie6";  
  
        # gzip_vary on;  
        # gzip_proxied any;  
        # gzip_comp_level 6;  
        # gzip_buffers 16 8k;  
        # gzip_http_version 1.1;  
        # gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;  
  
        ##  
        # Virtual Host Configs  
        ##  
  
        include /etc/nginx/conf.d/*.conf;  
        include /etc/nginx/sites-enabled/*;  
        #以下为我们添加的内容  
       server {               
              listen 80;  
              server_name your-ipaddress;  
  
              root /home/my-project/;  
              index index.html;  
              location /datas {  
              rewrite ^.+datas/?(.*)$ /$1 break;  
              include uwsgi_params;  
              proxy_pass http://ip:port;  
                              }  
             }  
}  
接下来就根据配置文件进行下一步工作。配置文件中的server_name后面是阿里云服务器的ip地址
3.配置文件中的listen是nginx监听的端口号，所以需要在阿里云服务器上为80端口添加安全组规则

在本地的浏览器登录阿里云服务器->进入控制台->点击安全组->点击配置规则->点击添加安全组规则，之后配置如下（注：入方向和出方向都要配置）



4.配置文件中的root和index那两行表示我们把项目文件夹放在/home/my-project下

例如有两个项目文件夹分别为test1，test2，里面都有index.html。则目录结构如下

/home

       |--my-project

              |--test1

                      |--index.html

              |--test2

                      |--index.html

则在浏览器输入http://ip/test1/index.html

服务器便会在/home/my-project中找到test1下的index.html执行；

如果在浏览器中输入http://ip/test2/index.html

服务器便会在/home/my-project中找到test2下的index.html执行；

这样便可以在服务器下放多个项目文件夹。

5.所以我们也需要在本地项目的config/index.js里的build下进行修改,如果要把项目放到test1下，则

[javascript] view plain copy
assetsPublicPath: '/test1/',  
如果用到了vue-router，则修改/router/index.js
[javascript] view plain copy
export default new Router({  
  base: '/test1/',   //添加这行  
  linkActiveClass: 'active',  
  routes  
});  
6.nginx配置文件中的location则是针对跨域处理，表示把对/datas的请求转发给http://ip:port,本文中这个http://ip:port下就是需要的数据，例如http://ip:port/seller,在本地项目文件中ajax请求数据的地方如下
[javascript] view plain copy
const url = '/datas/seller';  
this.$http.get(url).then((response) => {  
  .....  
});  
7.修改后在本地命令行下运行:cnpm run build 生成dist文件。把dist文件里的index.html和static文件上传到服务器的/home/my-project/test1下，目录结构如下
/home

       |--my-project

              |--test1

                      |--index.html

                      |--static

8.启动nginx

[plain] view plain copy
service nginx start  
9.至此项目部署成功，在浏览器下输入:  http://ip/test1/index.html  即可
