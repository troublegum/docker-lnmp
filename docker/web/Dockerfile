FROM alpine:3.14

# Install packages and remove default server definition
RUN apk --no-cache add \
  bash \
  curl \
  nginx \
  mc \  
  php8 \
  php8-ctype \
  php8-curl \
  php8-dom \
  php8-fpm \
  php8-gd \
  php8-intl \
  php8-json \
  php8-mbstring \
  php8-opcache \
  php8-openssl \
  php8-phar \
  php8-session \
  php8-xml \
  php8-simplexml \
  php8-xmlreader \
  php8-zlib \
  php8-intl \
  php8-iconv \
  php8-tokenizer \
  php8-pdo_mysql

# Create symlink so programs depending on `php` still function
RUN ln -s /usr/bin/php8 /usr/bin/php

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Init entrypoint script 
COPY entrypoint.sh /entrypoint.sh
RUN chmod 0755 /entrypoint.sh

# Configure PHP-FPM
COPY php.ini /etc/php8/conf.d/custom.ini

# Configure nginx
COPY nginx.conf /etc/nginx/http.d/default.conf

# Set default workdir
WORKDIR /var/www

# Run entrypoint bash script
ENTRYPOINT ["/entrypoint.sh"]
