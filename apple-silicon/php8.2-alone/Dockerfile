FROM php:8.2.4RC1-fpm

RUN set -ex

# ADD wget
RUN apt-get update
RUN  apt-get install -y wget
RUN apt-get -y install git

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
#
## ADD PHP Extension
RUN apt-get install -y --no-install-recommends libfreetype6-dev \
		libjpeg-dev \
		libmagickwand-dev \
		libpng-dev \
		libzip-dev

#RUN	docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr --with-png-dir=/usr
#RUN docker-php-ext-install gd
#
#RUN docker-php-ext-configure zip --with-libzip=/usr/include
RUN docker-php-ext-install zip
#
#RUN docker-php-ext-install pdo_mysql
#RUN docker-php-ext-install exif
#RUN docker-php-ext-install bcmath
#
## COPY ./testing /var/www/html
## COPY vhost.conf /etc/apache2/sites-available/000-default.conf
#RUN chown -R www-data:www-data /var/www/html && a2enmod rewrite
#
#RUN apt-get install --no-install-recommends --assume-yes --quiet ca-certificates curl git &&\
#    rm -rf /var/lib/apt/lists/*
#RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
#ENV PATH /usr/local/go/bin:$PATH
