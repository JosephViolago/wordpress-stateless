FROM wp-stateless-nginx:wp-4.8.3

# Install dockerize (https://github.com/jwilder/dockerize)
# ENV DOCKERIZE_RELEASE v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz
# RUN curl -sL https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_RELEASE} \
#   | tar -C /usr/bin -xzvf -

################################################################################
# WORDPRESS Config
################################################################################
# ADD ./wordpress/wp-config.php /var/www/html/wp-config.php
# chown wp-config.php to root
# RUN chown root:root /var/www/html/wp-config.php

################################################################################
# Configure and install WordPress
################################################################################
ARG MYSQL_HOST
ARG MYSQL_PORT
ARG MYSQL_USER
ARG MYSQL_PASSWORD
ARG MYSQL_DATABASE
# ARG WORDPRESS_URL
# ARG WORDPRESS_TITLE
# ARG WORDPRESS_ADMIN_USER
# ARG WORDPRESS_ADMIN_PASSWORD
# ARG WORDPRESS_ADMIN_MAIL

RUN wp config create \
    --dbhost=${MYSQL_HOST:-db}:${MYSQL_PORT:-3306} \
    --dbuser=${MYSQL_USER:-root} \
    --dbpass=${MYSQL_PASSWORD:-root} \
    --dbname=${MYSQL_DATABASE:-wp} \
    --skip-check
# Wait for the database to be ready
# RUN dockerize -wait tcp://${MYSQL_HOST:-db}:${MYSQL_PORT:-3306} -timeout 60s
# RUN wp core install \
#     --url=${WORDPRESS_URL:-localhost} \
#     --title=${WORDPRESS_TITLE:-'my-site'} \
#     --admin_user=${WORDPRESS_ADMIN_USER:-admin} \
#     --admin_password=${WORDPRESS_ADMIN_PASSWORD:-admin} \
#     --admin_email=${WORDPRESS_ADMIN_MAIL:-admin@example.com}
# && wp option update permalink_structure '/%year%/%monthnum%/%day%/%postname%/' \
# CMD wp server --host=${WORDPRESS_URL:-localhost}

# chown wp-config.php to root
# RUN chown root:root /var/www/html/wp-config.php

################################################################################
# WORDPRESS Plugins Setup
################################################################################
RUN mkdir /plugins

# Add All Plugin Files but
# ADD ./wordpress/plugins/ /plugins

# Execute each on its own for better caching support
# RUN /plugins.sh /plugins/base
# RUN /plugins.sh /plugins/security

# Delete Plugins script and folder
# RUN rm /plugins.sh && rm /plugins -r

# ADD OWN CUSTOM PLUGINS
# ADD ./plugins /var/www/html/wp-content/plugins

################################################################################
# WORDPRESS Themes Setup
################################################################################
# ADD ./themes/my-theme /var/www/html/wp-content/themes/my-theme

