FROM php:7.4-fpm-alpine
COPY /src /work
COPY /docker/php/php.ini /usr/local/etc/php/php.ini
LABEL maintainer="ucan-lab <info@u-can.tech>"

SHELL ["/bin/ash", "-oeux", "pipefail", "-c"]

# tinker(psysh)
ARG PSYSH_DIR=/usr/local/share/psysh
ARG PSYSH_PHP_MANUAL=$PSYSH_DIR/php_manual.sqlite
ARG PHP_MANUAL_URL=http://psysh.org/manual/ja/php_manual.sqlite

# timezone
ARG TZ=Asia/Tokyo

# composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

RUN apk update
RUN apk add --update --no-cache --virtual=.build-dependencies \
    autoconf \
    gcc \
    g++ \
    make \
    tzdata \
    git
RUN apk add --update --no-cache \
    mysql-dev \
    icu-dev \
    libzip-dev \
    libpng-dev \
    oniguruma-dev
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
  echo ${TZ} > /etc/timezone
RUN docker-php-ext-install intl pdo pdo_mysql mbstring exif zip gd
#   docker-php-ext-enable xdebug && \
# RUN pecl install xdebug
# RUN git clone https://github.com/phpredis/phpredis.git /usr/src/php/ext/redis && \
#   apk del .build-dependencies && \
#   docker-php-ext-install intl pdo pdo_mysql mbstring zip bcmath redis && \
#   docker-php-ext-enable xdebug && \
#   mkdir $PSYSH_DIR && curl $PHP_MANUAL_URL -o $PSYSH_PHP_MANUAL
# RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
#   composer config -g process-timeout 3600 && \
#   composer config -g repos.packagist composer https://packagist.jp
COPY --from=composer /usr/bin/composer /usr/bin/composer
# RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
# php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
#   php composer-setup.php && \
#   # php composer-setup.php --version=1.2.2 && \
#   php -r "unlink('composer-setup.php');" && \
#   mv composer.phar /usr/local/bin/composer && \
#   cd /work && \
#   composer install
