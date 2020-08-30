FROM alpine
# Upgrade existing packages in the base image
RUN apk update 
RUN apk --no-cache upgrade
# Creat directory for apache2 to store PID file
RUN mkdir /run/apache2
# Install from packages with out caching install files
RUN apk add --no-cache sed openrc apache2 php7-apache2 libmcrypt-dev php7 php7-fpm php7-opcache php7-pdo_mysql php7-xml \
 php7-xmlrpc php7-json php7-soap php7-mbstring php7-pecl-mcrypt php7-pecl-memcache php7-mysqli php7-ctype
# Add php-fpm7 to autostart
RUN rc-update add php-fpm7 default
# Run httpd in foreground so that the container does not quit
CMD ["-D","FOREGROUND"]
# Srart httpd when container runs
ENTRYPOINT ["/usr/sbin/httpd"]
# Apache2 config file
COPY ./httpd.conf /etc/apache2/httpd.conf
# Copy backend files
COPY backend/ /var/www/localhost/htdocs/dtapi
# Copy frontend files
COPY frontend/ /var/www/localhost/htdocs/
# Acess for web users
RUN chown apache. -R /var/www/localhost/htdocs/