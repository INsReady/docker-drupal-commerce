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

# Currenly, we need D8.1-dev
RUN curl -fSL "https://ftp.drupal.org/files/projects/drupal-8.1.x-dev.tar.gz" -o drupal.tar.gz \
	&& tar -xz --strip-components=1 -f drupal.tar.gz \
	&& rm drupal.tar.gz \

# install Drupal Commerce 2.x http://docs.drupalcommerce.org/v2/install.html
RUN composer config repositories.drupal composer https://packagist.drupal-composer.org \
  && composer require "drupal/commerce 8.2.x-dev" \
  && chown -R www-data:www-data modules

# install Drupal Console for future use, from https://drupalconsole.com/
RUN curl https://drupalconsole.com/installer -L -o drupal.phar \
  && mv drupal.phar /usr/local/bin/drupal \
  && chmod +x /usr/local/bin/drupal

# DC2.x is still under active dev, xdebug is useful
RUN pecl install xdebug && \
  docker-php-ext-enable xdebug
