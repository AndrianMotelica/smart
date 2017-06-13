FROM php:7.0-apache
    
RUN apt-get update && \
    apt-get -y install vim git
RUN  rm -rf /var/www/html
RUN  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer 

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
RUN docker-php-ext-install pdo pdo_mysql
RUN service apache2 restart

WORKDIR /var/www/povarenok

#CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
CMD ["sh", "-c", "tail -f /dev/null"]
