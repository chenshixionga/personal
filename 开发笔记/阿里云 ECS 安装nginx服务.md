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
   
   
  ### 6.aginx配置文件 /etc/nginx/conf.d/default.conf
 ```
 server {
    listen       80;
    server_name  39.106.41.106;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /home/my-project;
        index  index.html index.htm;
    }

	location /erpApi {  
	  rewrite ^.+erpApi/?(.*)$ /$1 break;  
	  include uwsgi_params;  
	  proxy_pass http://erp.ijiaol.com:18010;  
    }  
    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
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
 ```
 
 接下来就根据配置文件进行下一步工作。配置文件中的server_name后面是阿里云服务器的ip地址,配置文件中的listen是nginx监听的端口号，所以需要在阿里云服务器上为80端口添加安全组规则
