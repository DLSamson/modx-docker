FROM php:8.4-fpm-alpine
WORKDIR /var/www/html

# Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# GD Image
RUN apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libzip-dev libjpeg-turbo-dev \
  && docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
  NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
  && docker-php-ext-install -j$(nproc) gd \
  && apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

# Extensions
RUN docker-php-ext-install mysqli pdo pdo_mysql zip
RUN docker-php-ext-configure pdo_mysql

CMD ["php-fpm"]