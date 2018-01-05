FROM php:7.2-zts-alpine

LABEL maintainer="steve-liu <steveliu5153@gmail.com>"

#国内优化
#RUN echo "http://mirrors.ustc.edu.cn/alpine/v3.6/main/" >/etc/apk/repositories \
    && echo "61.191.56.16 pear.php.net" >> /etc/hots

# install swoole
RUN apk update \ 
    && pear upgrade --force

#安装编译需要的东西
RUN apk add  gcc \
    autoconf  \
    libc-dev \
    make \
    linux-headers\
    #安装swoole
    && pecl install swoole \
    && docker-php-ext-enable swoole \ 
    #安装完就清理，减少空间占用
    && apk del  gcc \  
    autoconf  \
    libc-dev \
    make \
    linux-headers

# log to /mnt/www/log
VOLUME [ "/mnt/php" ]
RUN echo "error_log = /mnt/php/log/error.log" > /usr/local/etc/php/conf.d/log.ini

#start
EXPOSE 80
CMD [ "php", "/mnt/php/start.php" ]