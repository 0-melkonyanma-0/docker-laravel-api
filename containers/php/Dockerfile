FROM php:8.2-apache

RUN apt-get update && apt-get upgrade -y \
    && apt-get install apt-utils -y \
    #
    #    устанавливаем необходимые пакеты
    && apt-get install git zip vim libzip-dev libgmp-dev libffi-dev libssl-dev libpq-dev -y \
    #
    #    Включаем необходимые расширения
    && docker-php-ext-install -j$(nproc) sockets zip gmp pcntl bcmath ffi \
    #
    #    Расшерения через pecl ставятся так, то в php 8 pecl сейчас отсутствует, так что строки закоментированы
    #    && PHP_OPENSSL=yes pecl install ev \
    #    && docker-php-ext-enable ev \
    #
    #    Чистим временные файлы
    && docker-php-source delete \
    && apt-get autoremove --purge -y && apt-get autoclean -y && apt-get clean -y

RUN docker-php-ext-install \
    pdo_mysql \
    pdo_pgsql \
    && a2enmod \
    rewrite 

WORKDIR ${WORKDIR_PATH}
ENV APACHE_RUN_USER=#1000

EXPOSE 80