FROM php:8.4-apache

# Bật rewrite cho Laravel
RUN a2enmod rewrite

# Cài extension
RUN docker-php-ext-install pdo pdo_mysql

# Cài Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Trỏ Apache về public/
ENV APACHE_DOCUMENT_ROOT=/var/www/html/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' \
    /etc/apache2/sites-available/*.conf \
    /etc/apache2/apache2.conf

WORKDIR /var/www/html

COPY . .

RUN composer install

RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 775 storage bootstrap/cache

EXPOSE 80
