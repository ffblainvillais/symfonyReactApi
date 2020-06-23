FROM php:7.3.8-fpm

RUN apt-get update
RUN apt-get install -y --no-install-recommends vim curl debconf subversion git apt-transport-https apt-utils \
    build-essential locales acl mailutils wget zip unzip \
    gnupg gnupg1 gnupg2
RUN docker-php-ext-install pdo pdo_mysql
COPY php.ini /etc/php/7.3.8/php.ini
COPY php-fpm-pool.conf /etc/php/7.3.8/pool.d/www.conf

# Php librairies
RUN pecl install \
    apcu

RUN curl -sSk https://getcomposer.org/installer | php -- --disable-tls && \
   mv composer.phar /usr/local/bin/composer

RUN groupadd dev -g 999
RUN useradd dev -g dev -d /home/dev -m


RUN apt-get install sudo
RUN sudo apt-get install --yes nodejs
#RUN sudo apt-get install --yes npm
#RUN npm install yarn

# Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN sudo apt update && sudo apt install yarn

RUN rm -rf /var/lib/apt/lists/*
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen

WORKDIR /home/www/symfonyReactApi

EXPOSE 9000
CMD ["php-fpm"]
