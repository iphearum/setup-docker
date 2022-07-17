FROM php:8.1-fpm

# Set virable
ENV APP='app-001'
ENV WEBROOT='/var/www/html'
ENV APP_DIR=${WEBROOT}/${APP}
ENV NODE_VERSION='12.13.0'

# Set working directory
WORKDIR ${APP_DIR}

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libpq-dev \
    zlib1g-dev \
    libxml2-dev \
    libzip-dev \
    libonig-dev \
    zip \
    curl \
    unzip \
    git \
    vim \
    && apt-get autoremove

RUN docker-php-ext-install pdo pdo_pgsql

RUN docker-php-ext-configure gd --with-freetype --with-jpeg
# RUN docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql
RUN docker-php-ext-install pdo_mysql \
    -j$(nproc) \
    gd \
    mysqli \
    zip \
    pdo \
    pdo_pgsql \
    pgsql
RUN apt-get update

# Install Postgre PDO
RUN apt-get install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add user for laravel application
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# adding node and npm and use nvm
# RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
# ENV NVM_DIR=/root/.nvm
# RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
# RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
# RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
# ENV PATH="/root/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
# RUN node --version
# RUN npm --version

# Copy existing application directory contents
COPY . .
# RUN npm cache clean --force
RUN composer install --no-dev --optimize-autoloader
RUN composer dump-auto
RUN php artisan key:generate
RUN php artisan config:cache
RUN php artisan cache:clear
RUN php artisan view:clear
RUN php artisan route:clear
RUN php artisan optimize
# RUN php artisan migrate:fresh
# RUN npm install --prefix public
#RUN php artisan db:seed

#Open Permission derictory
RUN chown -R www:www \
    ${APP_DIR}/storage \
    ${APP_DIR}/bootstrap/cache

RUN chmod -R 777 \
    ${APP_DIR}/ \
    ${APP_DIR}/storage \
    ${APP_DIR}/bootstrap/cache

RUN mkdir -p ${APP_DIR}/storage/framework/{sessions,views,cache}
RUN chmod -R 777 ${APP_DIR}/storage/framework

# Change current user to www
USER www

# Expose port 9000 and start php-fpm server
# EXPOSE 9000
# CMD ["php-fpm", "&", "php", 'artisan', 'migrate']
