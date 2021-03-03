FROM drupal:9

# install the PHP extensions we need
RUN docker-php-ext-install bcmath

# install Drupal Commerce 2.x https://docs.drupalcommerce.org/commerce2/developer-guide/install-update/installation#existing-site
RUN composer config minimum-stability RC \
    && composer require "drupal/commerce"
