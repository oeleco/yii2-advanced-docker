FROM php:7.2-fpm

RUN apt-get update && apt-get install -y \
curl \
wget \
git \
unzip \
libfreetype6-dev \
libjpeg62-turbo-dev \
libxslt-dev \
libicu-dev \
libmcrypt-dev \
libxml2-dev \
&& docker-php-ext-install -j$(nproc) iconv mbstring mysqli pdo_mysql zip \
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl
RUN docker-php-ext-install xsl
RUN docker-php-ext-install soap

# Install composer
RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer --version=1.10.16 \
       && mkdir /run/php \
       && composer global require hirak/prestissimo

ADD php.ini /usr/local/etc/php/conf.d/40-custom.ini

WORKDIR /var/www/app

CMD ["php-fpm"]
