FROM php:7.4.3-apache

ARG HOST_USER_NAME
ARG HOST_USER_ID
ARG HOST_GROUP_NAME
ARG HOST_GROUP_ID

# Create e new groups the same as the host group, add host user to it and create home for host user
RUN groupadd -g "${HOST_GROUP_ID}" "${HOST_GROUP_NAME}" && \
    useradd -g ${HOST_GROUP_ID} -u ${HOST_USER_ID} -m ${HOST_USER_NAME}

# Change running user of Apache to host user and group to avoid permission problems (Apache default is www-data)
ENV APACHE_RUN_USER=${HOST_USER_NAME}
ENV APACHE_RUN_GROUP=${HOST_GROUP_NAME}

# Common tools
RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends \
    git nano less wget zip unzip \
	&& docker-php-ext-install mysqli pdo pdo_mysql \
    && rm -rf /var/lib/apt/lists/*

# mhsendmail form Mailhog
RUN wget https://github.com/mailhog/mhsendmail/releases/download/v0.2.0/mhsendmail_linux_amd64 \
    && chmod +x mhsendmail_linux_amd64 \
    && mv mhsendmail_linux_amd64 /usr/local/bin/mhsendmail

# Composer
COPY --from=composer:2 /usr/bin/composer /usr/local/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER 1

# wp cli
RUN wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
    && php wp-cli.phar --info \
    && chmod +x wp-cli.phar \
    && mv wp-cli.phar /usr/local/bin/wp

# xdebug and mod_rewrite enable
RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN a2enmod rewrite