FROM docker.io/wardenenv/php-fpm:7.4-magento2-xdebug3

USER root
RUN dnf install -y php-devel php-pear gcc make autoconf pkgconfig openssl-devel \
    && pecl channel-update pecl.php.net \
    && pecl install mongodb-1.15.0 \
    && echo "extension=mongodb.so" > /etc/php.d/20-mongodb.ini \
    && php -m | grep mongodb
USER www-data