FROM php:7.4-apache

RUN set -ex

#ADD wget / nano
RUN apt-get update
RUN apt-get install -y wget
RUN apt-get -y install git
RUN apt-get -y install nano
#ADD apache SSL et REWRITE modules
RUN a2enmod ssl
RUN a2enmod rewrite
#Copy CONFIG and CERTs
RUN mkdir -p /etc/apache2/ssl
COPY ./ssl/*.pem /etc/apache2/ssl/
COPY ./000-default.conf /etc/apache2/sites-available/000-default.conf

#ADD composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN EXPECTED_CHECKSUM="$(wget -q -O - https://composer.github.io/installer.sig)"
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN ACTUAL_CHECKSUM="$(php -r "echo hash_file('sha384', 'composer-setup.php');")"

RUN	if [ "$EXPECTED_CHECKSUM" != "$ACTUAL_CHECKSUM" ]; \
	then >&2 echo 'ERROR: Composer Invalid installer checksum'; \
		rm composer-setup.php; \
		exit 1; \
	fi

RUN php composer-setup.php --quiet
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

# ADD PHP Extension
RUN apt-get install -y --no-install-recommends libfreetype6-dev \
		libjpeg-dev \
		libmagickwand-dev \
		libpng-dev \
		libzip-dev

RUN	docker-php-ext-configure gd --with-freetype=/usr --with-jpeg=/usr
RUN docker-php-ext-install gd

# RUN docker-php-ext-configure zip --with-libzip=/usr/include
RUN docker-php-ext-install zip

RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install exif
RUN docker-php-ext-install bcmath
# HTML owned by www-data
RUN chown -R www-data:www-data /var/www/html

EXPOSE 80
EXPOSE 443
