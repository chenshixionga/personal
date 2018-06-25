### 1、注册阿里云账号，或者用其他账号登录

### 2、实例化ECS  选择系统linux

### 3、安装nginx 
   ##### ① yum install nginx
   ##### ② is this ok: y  
   
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
