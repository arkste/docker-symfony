FROM arkste/docker-ci:php80

ARG USER_ID=1000

RUN usermod -u $USER_ID www-data

RUN apt-get update \
    && apt-get install -y \
    php8.0-fpm \
    && apt-get autoremove -y \
    && apt-get clean

RUN version=$(php -r "echo PHP_MAJOR_VERSION.PHP_MINOR_VERSION;") \
    && curl -A "Docker" -o /tmp/blackfire-probe.tar.gz -D - -L -s https://blackfire.io/api/v1/releases/probe/php/linux/amd64/$version \
    && tar zxpf /tmp/blackfire-probe.tar.gz -C /tmp \
    && mv /tmp/blackfire-*.so $(php -r "echo ini_get('extension_dir');")/blackfire.so \
    && printf "extension=blackfire.so\nblackfire.agent_socket=tcp://blackfire:8707\n" > /etc/php/8.0/fpm/conf.d/blackfire.ini

RUN mkdir -p /run/php/ && touch /run/php/php8.0-fpm.pid && chown $USER_ID:www-data /run/php/php8.0-fpm.pid

WORKDIR /var/www

CMD ["php-fpm8.0", "-F"]

EXPOSE 9000 9001
