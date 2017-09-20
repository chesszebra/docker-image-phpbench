FROM chesszebra/php:7.1

# Run as root
USER root:root

# Update PECL and install XDebug
RUN pecl update-channels \
 && pecl install xdebug \
 && docker-php-ext-enable xdebug

# Copy over the configuration file for PHP
COPY usr/local/etc/php/php.ini /usr/local/etc/php/php.ini

# Install phpbench
RUN curl -o phpbench.phar https://phpbench.github.io/phpbench/phpbench.phar \
 && curl -o phpbench.phar.pubkey https://phpbench.github.io/phpbench/phpbench.phar.pubkey \
 && chmod 0755 phpbench.phar \
 && mv phpbench.phar /usr/local/bin/phpbench \
 && mv phpbench.phar.pubkey /usr/local/bin/phpbench.pubkey

# Run the container as the configured user
USER php:php

# Execute phpunit
ENTRYPOINT ["phpbench"]
