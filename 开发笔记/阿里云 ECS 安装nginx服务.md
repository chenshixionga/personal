### 1、注册阿里云账号，或者用其他账号登录

### 2、实例化ECS  选择系统linux

### 3、安装nginx 
   ####1.添加资源

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

   3.启动Nginx

   刚安装的Nginx不会自行启动。运行Nginx:
   ```
   sudo systemctl start nginx.service
   ``
   如果一切进展顺利的话，现在你可以通过你的域名或IP来访问你的Web页面来预览一下Nginx的默认页面
   
   
### 完全卸载掉nginx
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
