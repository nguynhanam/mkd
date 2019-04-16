FROM php:7.1-fpm
RUN apt-get update && apt-get install -y apt-utils
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libmcrypt-dev \
        libpng-dev \
        libcurl4-nss-dev \
        libxml2-dev \
        libxslt-dev \
        apt-utils \
        libjpeg-dev \
        libpq-dev \
        libmemcached-dev \
        curl \        
        libwebp-dev \	
        libjpeg62-turbo-dev \ 
        libpng-dev \
        libxpm-dev 
RUN docker-php-ext-install iconv \
    && docker-php-ext-install gd \
    && docker-php-ext-install curl \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install json \
    && docker-php-ext-install soap \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install xsl \
    && docker-php-ext-install intl \
    && docker-php-ext-install zip \
    && docker-php-ext-install bcmath
RUN DEBIAN_FRONTEND=noninteractive apt-get update 
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/lib/x86_64-linux-gnu --with-jpeg-dir=/usr/lib/x86_64-linux-gnu && docker-php-ext-install gd
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug
RUN docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install opcache
RUN curl -L -o /tmp/memcached.tar.gz "https://github.com/php-memcached-dev/php-memcached/archive/php7.tar.gz" \
    && mkdir -p /usr/src/php/ext/memcached \
    && tar -C /usr/src/php/ext/memcached -zxvf /tmp/memcached.tar.gz --strip 1 \
    && docker-php-ext-configure memcached \
    && docker-php-ext-install memcached \
    && rm /tmp/memcached.tar.gz
RUN docker-php-ext-enable memcached
RUN docker-php-ext-configure memcached --enable-memcached
RUN apt-get -y update 
RUN apt-get install -y unixodbc unixodbc-dev
RUN pecl install sqlsrv \
    && docker-php-ext-enable sqlsrv
RUN pecl install pdo_sqlsrv \
    && docker-php-ext-enable pdo_sqlsrv
RUN ACCEPT_EULA=y apt-get install -y gnupg2
RUN apt-get install -y apt-transport-https
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list
RUN apt-get update -yqq \
    && ACCEPT_EULA=Y apt-get install -y msodbcsql17 unixodbc-dev unixodbc \
    && rm -r /var/lib/apt/lists/*

RUN pecl install sqlsrv pdo_sqlsrv

RUN /usr/local/bin/docker-php-ext-enable sqlsrv pdo_sqlsrv
