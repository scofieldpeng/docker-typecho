# 为typecho构建的php-fpm镜像，因为官方的php镜像没有启动pod_mysql扩展，因此需要自行构建一个
FROM php:7.2.3-fpm
LABEL author scofieldpeng<penjianfeng@gmail.com
# 因为国内牛逼的互联网环境，将源镜像切换到阿里云镜像方便拉取
COPY ./source.list /etc/apt/source.list
# 安装pdo_mysql拓展
RUN apt-get update && docker-php-ext-install pdo_mysql



