FROM drupal:8.8

# install the PHP extensions we need
RUN apt-get update \
  && apt-get install -y git \
        && rm -rf /var/lib/apt/lists/* \
        && docker-php-ext-install bcmath

# install Composer globally
RUN curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer

# install Drupal Commerce 2.x https://docs.drupalcommerce.org/commerce2/developer-guide/install-update/installation
RUN  cd /var \
     && rm -rf /var/www \
     && composer create-project drupalcommerce/project-base www --stability dev \
     && ln -s /var/www/web /var/www/html \
     && chown -R www-data:www-data /var/www/web
