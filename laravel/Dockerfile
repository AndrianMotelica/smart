FROM php:7.0-apache
    
RUN apt-get update && \
    apt-get -y install vim git zlib1g-dev
RUN  rm -rf /var/www/html
RUN  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer 

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
RUN docker-php-ext-install zip pdo pdo_mysql

COPY ./runables/run.sh /opt/run.sh
RUN chmod +x /opt/run.sh \
    && a2enmod rewrite

WORKDIR /var/www/povarenok

CMD ["/opt/run.sh"]
