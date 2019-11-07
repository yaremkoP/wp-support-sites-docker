FROM php:7.1-fpm

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \     
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) mysqli
    
RUN pecl install redis-4.0.1 \
    && pecl install xdebug-2.6.0 \
    && docker-php-ext-enable redis xdebug
    
ADD xdebug.ini /etc/php7/php-fpm.d/
ADD xdebug.ini /etc/php7/cli/conf.d/
ADD xdebug.ini /etc/php7/conf.d/
ADD xdebug.ini /usr/local/etc/php/conf.d/

CMD ["php-fpm", "-F"]

EXPOSE 9000