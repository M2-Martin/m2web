ARG baseimage

FROM $baseimage

ARG domain

RUN apt -y update \
    && apt -y install libbz2-dev \
    && apt -y install libffi-dev \
    && apt -y install zlib1g-dev \
    && apt -y install libpng-dev \
    && apt -y install libldap2-dev \
    && apt -y install freetds-dev libsybdb5 \ 
    && apt -y install firebird-dev \
    && apt -y install libpq-dev \
    && apt -y install libpspell-dev \
    && apt -y install libxml2-dev \
    && apt -y install libxslt1-dev \
    && apt -y install libzip-dev
RUN ln -s /usr/lib/aarch64-linux-gnu/libsybdb.so /usr/lib
#RUN ln -s /usr/lib/libsybdb.a /usr/lib/
RUN docker-php-ext-install bcmath bz2 calendar dba exif ffi gd gettext ldap mysqli pcntl pdo_dblib pdo_firebird pdo_mysql pdo_pgsql pgsql pspell shmop soap sockets sysvmsg sysvsem sysvshm xmlrpc xsl zip opcache
#RUN docker-php-ext-install bcmath bz2 calendar dba exif ffi gd gettext ldap mysqli pcntl pdo_firebird pdo_mysql pdo_pgsql pgsql pspell shmop soap sockets sysvmsg sysvsem sysvshm xmlrpc xsl zip
RUN pecl install apcu \
    && pecl install apcu_bc-1.0.3 \
    && docker-php-ext-enable apcu --ini-name 10-docker-php-ext-apcu.ini \
    && docker-php-ext-enable apc --ini-name 20-docker-php-ext-apc.ini


RUN rm /usr/local/etc/php-fpm.d/*.conf
COPY ./php-pool.conf /usr/local/etc/php-fpm.d/php-pool.conf
RUN sed -i "s/DOMAIN/$domain/g" /usr/local/etc/php-fpm.d/php-pool.conf

