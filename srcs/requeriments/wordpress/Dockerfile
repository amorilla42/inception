FROM debian:bullseye

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -y \
	wget \
	php \
	php-fpm \
 	php-mysql \
	php-phar\
	mariadb-client \
	sendmail

RUN wget https://wordpress.org/wordpress-6.0.tar.gz -P /var/www

RUN cd /var/www && tar -xzf wordpress-6.0.tar.gz && rm wordpress-6.0.tar.gz

COPY ./conf/www.conf /etc/php/7.4/fpm/pool.d/www.conf 

RUN	chown -R root:root /var/www/wordpress

RUN wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar

RUN chmod +x wp-cli.phar

RUN mv wp-cli.phar /usr/local/bin/wp-cli.phar

COPY tools/auto_config.sh auto_config.sh

ENTRYPOINT ["bash", "auto_config.sh"]
