# Typecho-Docker

typecho的docker镜像和docker-compose包

> 一般项目我都习惯用英文的readme方便万一能帮助到其他语种的客户呢（其实是zhuang bi，哈哈哈)，不过想到用typecho的都是国人，懒得写英文的readme了，2333

## 使用

1. 下载typecho到当前目录，解压到typecho文件夹
2. 修改typecho.conf中的server_name为具体的域名
3. mysql.env中配置，具体详见mysql.env即可
3. 进入php文件夹，执行`docker build -t scofieldpeng/php-fpm:7.2.3-fpm .`
4. 返回项目根目录，然后执行`docker-compose up -d`即可
5. 在宿主机的nginx中新建相应的配置文件，proxy到8080即可
6. 初始化typecho配置

## 使用HTTPS

由于是采用的proxy到容器的80端口，因此typecho不会知道目前是用的https协议，通过源码可以看到，typecho支持显性告诉当前的域名是https，因此可以在typecho的index.php或者config.inc.php中添加下列代码:

```php
/** 开启https支持 **/
define('__TYPECHO_SECURE__',TRUE);
```

当然，如果你的服务器只需要跑一个博客，而不需要其他的服务在80或者443端口，直接修改typecho.conf，添加https，再修改docker-compose.yaml文件，暴露出80和443端口即可，这里不做详细阐述。

## 备份和恢复/迁移

备份很简单，直接将项目目录整个copy下来即可，恢复时整个文件夹上传到新的服务器，然后进入目录执行`docker-compose up -d`重新跑起来即可，方便快捷

## MYSQL管理

可以看到docker-compose中mysql镜像时暴露出了3306端口到127.0.0.1，可以通过ssh代理登录13306端口进行管理，也可以安装一个phpadmin的容器连接上，看自己方便啦！
