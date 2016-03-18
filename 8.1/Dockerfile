# from http://docs.drupalcommerce.org/commerce-2/install.html
FROM drupal:8.1

# install the PHP extensions we need
RUN apt-get update \
  && apt-get install -y unzip git \
        && rm -rf /var/lib/apt/lists/* \
        && docker-php-ext-install bcmath

# install Composer globally
RUN curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer

# download Drupal Commerce dependent modules and
RUN cd modules \
  && curl -fSL "http://ftp.drupal.org/files/projects/composer_manager-8.x-1.x-dev.tar.gz" -o composer_manager.tar.gz \
        && tar -xzf composer_manager.tar.gz \
        && curl -fSL "http://ftp.drupal.org/files/projects/commerce-8.x-2.x-dev.tar.gz" -o commerce.tar.gz \
        && tar -xzf commerce.tar.gz \
        && curl -fSL "http://ftp.drupal.org/files/projects/address-8.x-1.x-dev.tar.gz" -o address.tar.gz \
        && tar -xzf address.tar.gz \
        && curl -fSL "http://ftp.drupal.org/files/projects/entity-8.x-1.x-dev.tar.gz" -o entity.tar.gz \
        && tar -xzf entity.tar.gz \
        && curl -fSL "http://ftp.drupal.org/files/projects/state_machine-8.x-1.x-dev.tar.gz" -o state_machine.tar.gz \
        && tar -xzf state_machine.tar.gz \
        && curl -fSL "http://ftp.drupal.org/files/projects/inline_entity_form-8.x-1.x-dev.tar.gz" -o inline_entity_form.tar.gz \
        && tar -xzf inline_entity_form.tar.gz \
        && curl -fSL "https://ftp.drupal.org/files/projects/profile-8.x-1.x-dev.tar.gz" -o profile.tar.gz \
        && tar -xzf profile.tar.gz \
        && rm *.tar.gz \
        && cd .. \
        && chown -R www-data:www-data modules

# temporary workaround for composer issue until the next drupal release https://www.drupal.org/node/2664274
RUN cd .. \
  && curl -sSL "https://www.drupal.org/files/issues/2664274-37.patch" -o 2664274-37.patch \
  && git apply -v 2664274-37.patch
  && rm 2664274-37.patch

# install Drupal Console for future use, from https://drupalconsole.com/
RUN curl https://drupalconsole.com/installer -L -o drupal.phar \
  && mv drupal.phar /usr/local/bin/drupal \
  && chmod +x /usr/local/bin/drupal

# DC2.x is still under active dev, xdebug is useful
RUN pecl install xdebug && \
  docker-php-ext-enable xdebug

# initialize Composer Manager to download external libraries
RUN php modules/composer_manager/scripts/init.php \
  && composer drupal-update -v
