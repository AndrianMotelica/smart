FROM php:7.1-apache
    
RUN apt-get update && \
    apt-get -y install vim git zlib1g-dev
RUN  rm -rf /var/www/html
RUN  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer 

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

# install container dependencies
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install zip pdo pdo_mysql

# manage runable command file
COPY ./runables/run.sh /opt/run.sh
RUN chmod +x /opt/run.sh \
    && a2enmod rewrite

WORKDIR /var/www/smart
RUN mkdir /var/www/smart/storage && \
    chmod +x /var/www/smart/storage

CMD ["/opt/run.sh"]
