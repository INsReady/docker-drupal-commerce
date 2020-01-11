FROM insready/drupal-dev:8.8

# install the PHP extensions we need
RUN docker-php-ext-install bcmath

# install Drupal Commerce 2.x https://docs.drupalcommerce.org/commerce2/developer-guide/install-update/installation
RUN  cd /var \
     && rm -rf /var/www \
     && composer create-project drupalcommerce/project-base www --stability dev \
     && ln -s /var/www/web /var/www/html \
     && chown -R www-data:www-data /var/www/web
