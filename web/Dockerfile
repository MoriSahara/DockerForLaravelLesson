FROM php:7.1-apache

WORKDIR /var/www/myblog
EXPOSE 80

COPY ./conf/php.ini /usr/local/etc/php/php.ini
COPY ./conf/apache2.conf /etc/apache2/apache2.conf
COPY ./conf/000-default.conf /etc/apache2/sites-available/000-default.conf


RUN apt-get update \
    && apt-get install -y \
    curl \
    wget \
    vim \
    sqlite3 \
    unzip \
    git
RUN  a2enmod rewrite

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1
