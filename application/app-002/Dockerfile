FROM php:8.1-fpm

ENV APP='app-001'
ENV WEBROOT='/var/www/html'
ENV APP_DIR=${WEBROOT}/${APP}

WORKDIR ${APP_DIR}

# RUN apt-get update && apt-get install -y \
#     git \
#     curl \
#     libpng-dev \
#     libonig-dev \
#     libxml2-dev \
#     zip \
#     unzip \
#     libpq-dev \
#     vim

# # nodejs \
# # Clear cache
# RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# # Install PHP extensions
# # RUN docker-php-ext-install pdo_mysql mbstring exif \
# # pcntl \
# # bcmath \
# # gd

# RUN curl -sL https://deb.nodesource.com/setup_16.x | bash -
# RUN docker-php-ext-install \
#     gd \
#     pdo \
#     pgsql \
#     pdo_pgsql

# # xml \
# # mbstring \
# # Set working directory

# # Install composer
# RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# # Add user for laravel application
# RUN groupadd -g 1000 www
# RUN useradd -u 1000 -ms /bin/bash -g www www

# # adding node and npm and use nvm
# # ENV NODE_VERSION=12.13.0
# # RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
# # ENV NVM_DIR=/root/.nvm
# # RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
# # RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
# # RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
# # ENV PATH="/root/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
# # RUN node --version
# # RUN npm --version

# # Copy existing application directory contents
# COPY . .
# # RUN npm cache clean --force
# RUN composer install
# RUN php artisan key:generate
# RUN composer dumpautoload
# RUN php artisan config:cache
# RUN php artisan cache:clear
# RUN php artisan view:clear
# RUN php artisan route:clear
# RUN php artisan optimize
# # RUN php artisan migrate
# # RUN npm install --prefix public
# #RUN php artisan db:seed

# #Open Permission derictory
# RUN chown -R www:www \
#     ${APP_DIR}/storage \
#     ${APP_DIR}/bootstrap/cache

# RUN chmod -R 777 \
#     ${APP_DIR}/ \
#     ${APP_DIR}/storage \
#     ${APP_DIR}/bootstrap/cache

# RUN mkdir -p ${APP_DIR}/storage/framework/{sessions,views,cache}
# RUN chmod -R 777 ${APP_DIR}/storage/framework

# # Change current user to www
# USER www

# # Expose port 9000 and start php-fpm server
# EXPOSE 9000
# CMD ["php-fpm"]
