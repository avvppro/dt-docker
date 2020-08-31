FROM alpine:3.12.0
# Upgrade existing packages in the base image
RUN apk update && apk --no-cache upgrade
RUN apk add --no-cache apache2
# Apache2 config file (Allow ovverride + mod_rewrite enable)
COPY ./httpd.conf /etc/apache2/httpd.conf
# Copy frontend files (build vs 172.33.0.5/dtapi & no .htaccess)
COPY artefact/ /var/www/localhost/htdocs/
# Acess for web users
RUN chown apache. -R /var/www/localhost/htdocs/
# Run httpd in foreground so that the container does not quit
CMD ["-D","FOREGROUND"]
# Start httpd when container runs
ENTRYPOINT ["/usr/sbin/httpd"]