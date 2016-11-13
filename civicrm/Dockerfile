# install auto de Drupal? avec Drush ? qu de localhost vs 192.168... sur Mac/Windows
# config de civicrm ?

##############################################
#  
FROM php:5.6-apache

RUN a2enmod rewrite
  
# install the PHP extensions we need
RUN apt-get update && apt-get install -y libpng12-dev libjpeg-dev libpq-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install gd mbstring pdo pdo_mysql pdo_pgsql zip                
WORKDIR /var/www/html 

ENV DRUPAL_VERSION 7.50
ENV DRUPAL_MD5 f23905b0248d76f0fc8316692cd64753 

# Workaround for write permission on write to MacOS X volumes
# See https://github.com/boot2docker/boot2docker/pull/534
RUN usermod -u 1000 www-data

RUN curl -fSL "http://ftp.drupal.org/files/projects/drupal-${DRUPAL_VERSION}.tar.gz" -o drupal.tar.gz \
    && echo "${DRUPAL_MD5} *drupal.tar.gz" | md5sum -c - \
    && tar -xz --strip-components=1 -f drupal.tar.gz \
    && rm drupal.tar.gz \
    && chown -R www-data:www-data sites \
    && chown -R www-data:www-data sites/default

##############################################
# civicrm's specific config

# Install PDO MySQL driver
# See https://github.com/docker-library/php/issues/62
RUN docker-php-ext-install pdo mysql
RUN docker-php-ext-install pdo mysqli

#Configure PHP memory limit
RUN {  \
        echo "memory_limit = 512M"; \
    } >> /usr/local/etc/php/php.ini

RUN chmod 755 /var/www/html/sites/default

##############################################
# Download civicrm to Drupal's module directory
# download: https://civicrm.org/download/list
# installation : https://wiki.civicrm.org/confluence/display/CRMDOC/Installing+CiviCRM+for+Drupal+7
RUN curl -L  https://download.civicrm.org/civicrm-4.7.13-drupal.tar.gz | tar zx -C /var/www/html/sites/all/modules
