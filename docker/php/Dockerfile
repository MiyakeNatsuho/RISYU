#FROM php:7-apache
FROM php:7.2-apache
# Install all required extensions and composer
ENV TZ Asia/Tokyo
RUN requirements="libicu63 libicu-dev g++ libxml2-dev libpng16-16 libpng-dev zlib1g-dev libjpeg-dev" \
  && apt-get update && apt-get install -y $requirements \
  && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
  && docker-php-ext-install -j$(nproc) pdo_mysql mbstring intl simplexml gd zip opcache exif\
  && requirementsToRemove="libicu-dev g++ libxml2-dev zlib1g-dev" \
  && apt-get purge --auto-remove -y $requirementsToRemove \
  && curl -sSL https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  && a2enmod remoteip \
  && a2enmod rewrite \
  # && pecl install xdebug \
  # && docker-php-ext-enable xdebug \
  && cp /usr/share/zoneinfo/Japan /etc/localtime \
  && apt-get update && apt-get install -y imagemagick libmagickwand-dev \
  && pecl install imagick \
  && docker-php-ext-enable imagick \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get update && apt-get install -y busybox-static
  