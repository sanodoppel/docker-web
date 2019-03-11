FROM php:7.3-fpm

RUN apt-get update && apt-get install -y nano sudo wget apt-utils

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get install -y libpq-dev libpng-dev libjpeg-dev libzip-dev libxml2-dev zip && docker-php-ext-configure zip --with-libzip

RUN docker-php-ext-install json opcache session mbstring pdo xml pdo_pgsql pdo_mysql pgsql mysqli gd mbstring zip

RUN pecl install redis xdebug mongodb
RUN docker-php-ext-enable redis xdebug mongodb

RUN wget https://phar.phpunit.de/phpunit.phar
RUN chmod +x phpunit.phar
RUN mv phpunit.phar /usr/local/bin/phpunit

RUN echo "www-data:www-data" | chpasswd && adduser www-data sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER www-data

WORKDIR /var/www

CMD ["php-fpm"]
