FROM php:7.1-apache
MAINTAINER flashvnn

VOLUME /var/www/html

RUN apt-get update && apt-get install -y libpng12-dev libjpeg-dev libpq-dev libxml2-dev \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
	&& docker-php-ext-install gd mbstring pdo pdo_mysql pdo_pgsql zip \
	&& docker-php-ext-install opcache bcmath soap \
  && pecl install redis-3.1.1 \
  && docker-php-ext-enable redis \
	&& a2enmod rewrite \
	&& rm -rf /var/lib/apt/lists/*
	
RUN yes | pecl install xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini
    
COPY drupal-*.ini /usr/local/etc/php/conf.d/
