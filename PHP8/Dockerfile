# Use an official PHP runtime as a parent image
FROM php:8.2-fpm

# Set working directory
WORKDIR /var/www/html

# Install Nginx
RUN apt-get update && apt-get install -y nginx

# Download nginx.conf using curl and place it in /etc/nginx/conf.d/
RUN curl -o /etc/nginx/nginx.conf https://minio.internal.codebuckets.in/public-tools-config/nginx/php8/nginx.conf

# Copy the current directory contents into the container at /var/www/html
COPY . /var/www/html

# Set the correct permissions
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

# Expose port 80
EXPOSE 80

# Start Nginx and PHP-FPM
CMD ["sh", "-c", "php-fpm -D && nginx -g 'daemon off;'"]
