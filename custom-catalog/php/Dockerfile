FROM php:7.1-fpm

RUN apt-get update \
  && apt-get install -y \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libxslt1-dev \
    libpng-dev \
    sudo \
    libfreetype6-dev \
    git

RUN apt-get -y install openssl && apt-get -y install vim

RUN docker-php-ext-install \
  bcmath \
  dom \
  gd \
  intl \
  mbstring \
  mcrypt \
  pdo_mysql \
  soap \
  xsl \
  zip \
  bcmath \
  iconv

RUN apt-get update && \
    apt-get install && \
    curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN  apt-get install -y mysql-client

RUN echo 'memory_limit = 2G\n\
max_execution_time = 1800\n\
zlib.output_compression = On' >> /usr/local/etc/php/php.ini

COPY ./src /var/www/html/application
RUN echo "www-data ALL = NOPASSWD: ALL" >> /etc/sudoers 	

WORKDIR /var/www/html/application
RUN find . -type d -exec chmod 700 {} \; && find . -type f -exec chmod 600 {} \;
RUN composer update
RUN php bin/magento sampledata:deploy
#RUN php bin/magneto deploy:mode:set developer
USER root
RUN chown :www-data .
EXPOSE 80    

