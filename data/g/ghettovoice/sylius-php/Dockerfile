FROM php:7.2-fpm  
  
RUN \  
apt-get update && \  
apt-get install -y \  
curl \  
wget \  
git  
  
RUN curl -sS https://getcomposer.org/installer | php -- --install-
dir=/usr/local/bin --filename=composer  
  
RUN apt-get update && apt-get install -y \  
libfreetype6-dev \  
libjpeg62-turbo-dev \  
libmcrypt-dev \  
libpng-dev \  
libicu-dev \  
libicu57 \  
libpq-dev \  
&& docker-php-ext-install iconv \  
&& docker-php-ext-install exif \  
&& docker-php-ext-install mbstring \  
&& docker-php-ext-install pdo_mysql \  
&& docker-php-ext-install pdo_pgsql \  
&& docker-php-ext-install pdo \  
&& docker-php-ext-install intl \  
&& docker-php-ext-install opcache \  
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-
dir=/usr/include/ \  
&& docker-php-ext-install gd \  
&& docker-php-ext-install zip  
  
EXPOSE 9000  

