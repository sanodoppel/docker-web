FROM php:7.4-fpm
ARG TIMEZONE

RUN apt-get update && apt-get install nano sudo

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone \
  && printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN  apt-get update && \
    apt-get install -y libpq-dev \
  libxml2-dev \
  libzip-dev \
  libpng-dev \
  libjpeg-dev \
  zip \
  && docker-php-ext-configure zip \
  && docker-php-ext-configure gd \
  && docker-php-ext-install \
    zip \
    gd \
    pdo_mysql \
    pdo_pgsql \
    bcmath \
    opcache

RUN apt-get install -y autoconf g++ make git \
  && docker-php-source extract \
  && pecl install \
    redis \
  && docker-php-ext-enable \
    redis \
  && docker-php-source delete \
  && mkdir /xdebug_installer && cd /xdebug_installer && git clone https://github.com/xdebug/xdebug.git && cd xdebug && sh ./rebuild.sh && cd / && rm -rf /xdebug_installer \
  && rm -rf /tmp/*

COPY conf.d/* /usr/local/etc/php/conf.d/

RUN echo "www-data:www-data" | chpasswd && adduser www-data sudo

RUN usermod -u 1001 www-data

RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER www-data

WORKDIR /var/www