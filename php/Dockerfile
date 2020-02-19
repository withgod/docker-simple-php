FROM php:7.2-apache

#COPY ./php.ini /usr/local/etc/php/
#COPY ./*.conf /etc/apache2/sites-enabled/

RUN apt-get update \
    && apt-get install -y git curl unzip netcat

RUN apt-get update \
    && apt-get install -y libmemcached-dev zlib1g-dev\
    && pecl install memcached-3.1.4 \
    && docker-php-ext-enable memcached \
    && docker-php-ext-install opcache \
    && docker-php-ext-install zip \
    && docker-php-ext-install mbstring

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
# skip check
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

WORKDIR /var/tmp/app

RUN rm -rf /var/www/html
RUN ln -sf /var/tmp/app/public /var/www/html 

CMD ["apache2-foreground"]
