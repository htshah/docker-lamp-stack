FROM php:7.2.1-apache
MAINTAINER egidio docile
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  # Make sure we're installing what we think we're installing!
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" \
  && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer --snapshot \
  && rm -f /tmp/composer-setup.*
RUN apt-get update
RUN apt-get -y install git libxml2-dev libzip-dev

RUN docker-php-ext-install pdo pdo_mysql mysqli
RUN docker-php-ext-install dom
RUN docker-php-ext-install xml
RUN docker-php-ext-install json
RUN docker-php-ext-install mbstring
RUN docker-php-ext-configure zip --with-libzip && \
  docker-php-ext-install zip

RUN a2enmod rewrite
RUN apt-get install -y nano
ENV APACHE_LOG_DIR /var/log/apache2
#ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf
Add php.ini /usr/local/etc/php/

RUN apt-get install -y libpng-dev
RUN docker-php-ext-install gd