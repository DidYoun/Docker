# Base
FROM php:7.0-fpm
# Author
MAINTAINER Didier Youn <didier.youn@gmail.com>
# Get packages extensions
RUN apt-get update && apt-get install -y \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        libssl-dev \
        libmemcached-dev \
        libz-dev \
        libmysqlclient18 \
        zlib1g-dev \
        libsqlite3-dev \
        zip \
        libxml2-dev \
        libcurl3-dev \
        libedit-dev \
        libpspell-dev \
        libldap2-dev \
        unixodbc-dev \
        libicu-dev \
        g++ \
        libpq-dev
# Xdebug
RUN pecl install xdebug-2.5.0 
# https://bugs.php.net/bug.php?id=49876
RUN ln -fs /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/
# Install PHP extensions
RUN echo "Installing PHP extensions" \
    && docker-php-ext-install -j$(nproc) iconv mcrypt intl gd pdo_mysql pdo_pgsql pcntl pdo_sqlite zip curl bcmath opcache simplexml xmlrpc xml soap session readline pspell ldap mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-enable intl xdebug iconv mcrypt gd pdo_mysql pdo_pgsql pcntl pdo_sqlite zip curl bcmath opcache simplexml xmlrpc xml soap session readline pspell ldap mbstring \
    && apt-get clean all 
# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --filename=composer --install-dir=/bin
ENV PATH /root/.composer/vendor/bin:$PATH
# Expose port
EXPOSE 9000
# Copy custom php.ini
COPY ./conf/php.ini /usr/local/etc/php/conf.d/php.ini