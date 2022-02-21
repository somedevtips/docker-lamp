FROM php:7.4.3-apache

ARG HOST_USER_NAME
ARG HOST_USER_ID
ARG HOST_GROUP_NAME
ARG HOST_GROUP_ID

RUN groupadd -g "${HOST_GROUP_ID}" "${HOST_GROUP_NAME}" && \
    useradd -g ${HOST_GROUP_ID} -u ${HOST_USER_ID} -m ${HOST_USER_NAME}

RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends \
    git nano less \
	&& docker-php-ext-install mysqli pdo pdo_mysql \
    && rm -rf /var/lib/apt/lists/*