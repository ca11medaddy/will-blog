---
summary: 实验室项目需要加一个网页前端，前段时间成功部署，这两天发现教程链接失效了，决定自己记录一下，方便以后回顾.
authors:
  - 阿威
lastMod: 2019-09-05T00:00:00.000Z
title: vue项目部署到阿里云服务器上
subtitle: 实验室项目需要加一个网页前端，前段时间成功部署，这两天发现教程链接失效了，决定自己记录一下，方便以后回顾。
date: 2020-09-30T00:00:00.000Z
tags: []
categories: []
projects: []
image:
  caption: ""
  focal_point: ""
---
## 需要的东西

[nginx](http://nginx.org/en/download.html)
[Xshell+Xftp](https://www.netsarang.com/zh/free-for-home-school/)

## 连接服务器

Xshell和Xftp连接服务器，主机名为服务器ip，账号密码对应
nginx下载到本地，再通过Xftp上传到服务器



![xftp上传nginx包](https://img-blog.csdnimg.cn/2020092415583388.png#pic_center)

## 安装gcc和g++编辑器



```javascript
javascript
yum -y install gcc automake autoconf libtool make
yum install gcc gcc-c++

```

## 解压nginx安装包

```javascript
tar -zxvf nginx-1.8.1.tar.gz
```

### 进入nginx-1.8.1目录

```javascript
cd nginx-1.8.1
```

### make编译安装它

```javascript
./configure
make
make install
```

## 安装zlib库

```javascript
cd ~
wget http://www.zlib.net/zlib-1.2.11.tar.gz
tar -zxvf zlib-1.2.11.tar.gz
cd zlib-1.2.11
./configure
make
make install
```

### 安装 SSL

```javascript
yum -y install openssl openssl-devel
```

### 安装 pcre

```javascript
yum -y install pcre-devel
```

### 安装 nginx

```javascript
./configure
make
make install
```

## nginx 服务的基本操作

### 启动服务

```javascript
/usr/local/nginx/sbin/nginx
```

这个时候访问你服务器的公用 ip 地址，如果可以打开下面这样一个页面，说明 nginx 启动成功
![nginx配置成功](https://img-blog.csdnimg.cn/20200924161827385.png#pic_center)

### 重启服务

```javascript
/usr/local/nginx/sbin/nginx -s reopen
```

### 查看服务

```javascript
ps -ef | grep nginx
```

![查看服务](https://img-blog.csdnimg.cn/20200924161933478.png#pic_center)

红框中的数字在停止服务时会用到

### 停止服务

```javascript
kill 7332
```

### 查看配置

```javascript
vi /usr/local/nginx/conf/nginx.conf
```

### 重新载入配置

在修改配置文件之后需要重新载入配置文件

```javascript
/usr/local/nginx/sbin/nginx -s reload
```

## 打包vue项目并上传到服务器

执行 **npm run build**打包项目，打包成功之后，会在项目目录下多出一个**dist**文件夹，里面有一个**static**目录(存放有静态文件)和**index.html**，这就是打包以后的项目，用xftp把这个文件夹上传到服务器。待传输完成之后，打开xshell，运行

```javascript
vim /usr/local/nginx/conf/nginx.conf
```

修改nginx的配置文件(`vi里键入a进入编辑模式，修改完成后esc将光标移到文末，再键入:wq即可保存`)
![修改配置文件](https://img-blog.csdnimg.cn/20200924162532896.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXNodWFpNjY2,size_16,color_FFFFFF,t_70#pic_center)

在server的location中配置站点根目录,修改完成之后需要重新载入配置文件

```javascript
/usr/local/nginx/sbin/nginx -s reload
```

**此时访问服务器ip地址就可以看到部署成功的项目了。**

## 可能出现的问题及解决方法

### 404或405

vue配置了跨域，可能会导致访问出现404或405等错误，因为vue配置的跨域只能在本地生效，打包之后就失效了，给nginx配置跨域即可解决。

### 403

权限错误，将nginx.config的user设置为启动用户

### nginx 报异常"/usr/local/nginx/logs/nginx.pid" failed (2: No such file or directory)

可能是nginx.conf的nginx.pid被注释了，把配置文件中pid前的#去掉保存退出重启即可