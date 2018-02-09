FROM php:7.1-apache
MAINTAINER flashvnn

VOLUME /var/www/html

COPY drupal-*.ini /usr/local/etc/php/conf.d/

RUN apt-get update && apt-get install -y libpng12-dev libjpeg-dev libpq-dev libxml2-dev \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
	&& docker-php-ext-install gd mbstring pdo pdo_mysql pdo_pgsql zip \
	&& docker-php-ext-install opcache bcmath soap \
  && pecl install redis-3.1.1 \
  && docker-php-ext-enable redis \
	&& a2enmod rewrite \
	&& rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install sudo && apt-get install wget -y

RUN curl -sS https://getcomposer.org/installer | sudo php -d allow_url_fopen=On -- --install-dir=/usr/local/bin --filename=composer

RUN curl https://drupalconsole.com/installer -L -o ~/drupal.phar

RUN mv ~/drupal.phar /usr/local/bin/drupal

RUN chmod +x /usr/local/bin/drupal

RUN composer global require drush/drush

RUN apt-get install git -y