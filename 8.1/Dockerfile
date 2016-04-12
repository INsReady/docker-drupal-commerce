FROM drupal:8.1

# install the PHP extensions we need
RUN docker-php-ext-install bcmath

# install Composer globally
RUN curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer

# install Drupal Commerce 2.x http://docs.drupalcommerce.org/v2/install.html
RUN composer config repositories.drupal composer https://packagist.drupal-composer.org \
  && composer require "drupal/commerce 8.2.x-dev" --prefer-dist \
  && chown -R www-data:www-data modules
