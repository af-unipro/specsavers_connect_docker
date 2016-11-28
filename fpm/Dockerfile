FROM ssuatdockerreg.theuniprogroup.com/php:15.03-5.6.5-fpm-mod10
	
RUN apt-get update && \
    apt-get install -y curl nano mysql-client && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer	

RUN export PATH="$HOME/.composer/vendor/bin:$PATH"
RUN composer global require drush/drush

# Create and/or navigate to a path for the single Composer Drush install.
RUN mkdir --parents /opt/drush-8.x
RUN cd /opt/drush-8.x
# Initialise a new Composer project that requires Drush.
RUN composer init --require=drush/drush:8.* -n
# Configure the path Composer should use for the Drush vendor binaries.
RUN composer config bin-dir /usr/local/bin
# Install Drush. 
RUN composer install

COPY ./drushrc.php ~/.drush/

RUN mkdir -p /data/shared/tmp && mkdir -p /data/shared/private

RUN chown www-data:staff /tmp /data/shared/tmp /data/shared/private
RUN chmod -R 0777 /tmp /var/www/html /data/shared/tmp /data/shared/private
RUN usermod -u 1000 www-data

WORKDIR /var/www/html
