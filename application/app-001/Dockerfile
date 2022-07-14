FROM phpdockerio/php80-fpm:latest
WORKDIR "/"

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php8.1-pgsql php8.1-gd php-redis \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install git
RUN apt-get update \
    && apt-get -y install git \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

COPY . .
RUN composer install --ignore-platform-reqs

# RUN chmod -R 777 /home
# RUN composer install
RUN php artisan key:generate
RUN php artisan optimize
# RUN php artisan config:cache
# RUN php artisan config:clear
# RUN php artisan cache:clear
# RUN composer update
# RUN php artisan migrate
# RUN php artisan seed

EXPOSE 9000
# CMD ["php-fpm"]
