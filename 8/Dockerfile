# from http://docs.drupalcommerce.org/commerce-2/install.html
FROM drupal:8.0

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
	&& curl -fSL "http://ftp.drupal.org/files/projects/inline_entity_form-8.x-1.x-dev.tar.gz" -o inline_entity_form.tar.gz \
	&& tar -xzf inline_entity_form.tar.gz \
	&& rm *.tar.gz \
	&& git clone https://github.com/fago/profile2.git --branch=8.x-1.x ./profile \
	&& cd .. \
	&& chown -R www-data:www-data modules

# install Drupal Console for future use
RUN curl -LSs http://drupalconsole.com/installer | php \
  && mv console.phar /usr/local/bin/drupal

# initialize Composer Manager to download external libraries
RUN php modules/composer_manager/scripts/init.php \
  && composer drupal-update
