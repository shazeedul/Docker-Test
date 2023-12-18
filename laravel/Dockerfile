# Use the official PHP image
FROM php:8.2-fpm

# Set the working directory in the container
WORKDIR /app/laravel

# Install dependencies
RUN apt update && apt install -y \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    ca-certificates \
    gnupg \
    libonig-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libmariadb-dev \
    libicu-dev

# Install PHP extensions
RUN docker-php-ext-install mbstring pdo pdo_mysql gd mysqli

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Node.js and npm
RUN curl -sL https://deb.nodesource.com/setup_20.x | bash -
RUN apt-get install -y nodejs

# Copy the application files to the container
COPY . .

# Copy the composer.json and composer.lock
COPY composer.json composer.lock ./

# Install the PHP dependencies
RUN composer install

# Install the node_module dependencies
RUN npm install

# Generate the Laravel application key
RUN php artisan key:generate

# Expose port 8000 and start the PHP server
EXPOSE 8000
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]
