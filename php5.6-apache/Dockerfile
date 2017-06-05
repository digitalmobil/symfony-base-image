# TODO there needs to be a web server one day..
FROM php:7.1

MAINTAINER {klaus.hartl,roland.tuschl}@digitalmobil.com

# Enable Apache Rewrite Module
#RUN a2enmod rewrite

RUN apt-get update -yqq \
    && apt-get install -yqq \
        git libmcrypt-dev libpq-dev libcurl4-gnutls-dev libicu-dev libvpx-dev libjpeg-dev libpng-dev libxpm-dev zlib1g-dev libfreetype6-dev libxml2-dev libexpat1-dev libbz2-dev libgmp3-dev libldap2-dev unixodbc-dev libsqlite3-dev libaspell-dev libsnmp-dev libpcre3-dev libtidy-dev \
        libc-client-dev libkrb5-dev libssl-dev libwebp-dev unzip zip \
        cron \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#RUN docker-php-ext-configure imap --with-imap --with-imap-ssl --with-kerberos

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# TODO maybe add xdebug for test image
RUN docker-php-ext-install bz2 curl gd intl json mbstring mcrypt mysqli opcache pdo pdo_mysql xml zip

RUN { \
    echo 'date.timezone = "Europe/Berlin"';     \
    echo 'upload_max_filesize = 20M';           \
    echo 'post_max_size = 20M';                 \
    echo 'memory_limit = 512M';                 \
    } > /usr/local/etc/php/conf.d/symfony.ini

RUN sed -i -E 's/(session\s*required\s*pam_loginuid.so)/#\1/' /etc/pam.d/cron

# CMD ["apache2-foreground"]
