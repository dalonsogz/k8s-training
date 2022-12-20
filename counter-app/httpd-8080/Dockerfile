FROM alpine:3.15

RUN apk add apache2 php7-apache2 php7-mongodb curl --update-cache --no-cache            

RUN mkdir -p /run/apache2/ && \
    rm -r /var/www/localhost/htdocs/* && \
    chown -R apache:apache /var/www/ /var/log/apache2 /usr/lib/apache2 /run/apache2 && \
    ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log && \
    sed -i 's/Listen 80/Listen 0.0.0.0:8080/g' /etc/apache2/httpd.conf
#    sed -i 's/#LoadModule rewrite_module/LoadModule rewrite_module/g' /etc/apache2/httpd.conf && \
#    sed -i 's/AllowOverride None/AllowOverride All/1' /etc/apache2/httpd.conf

COPY ["index.php", "/var/www/localhost/htdocs/"]
ENV MONGO_CS="mongodb://localhost:27017"

EXPOSE 8080
USER apache
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
