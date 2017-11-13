
# Wordpress Stateless

Dockerfiles for a custom Wordpress Setup that is fully Stateless.

## base

Contains the Wordpress installation and some additional scripts for plugins setup and variable config filtering.
Includes PHP-FPM.

## cli

Adds WP-CLI to the Dockerfile to use for maintainance operations on the Wordpress installation Database.

## nginx

Installs NGINX and adds configuration to call PHP-FPM.

## setup

Setup Script for a fresh wordpress setup via the WP-CLI docker container.

## Install

```bash
git clone git@github.com:JosephViolago/wordpress-stateless.git
cd wordpress-stateless
./build-images.sh 4.8.3 8efc0b9f6146e143ed419b5419d7bb8400a696fc
cd pdf-search
docker-compose up --build -d

docker-compose exec --user root wordpress bash -c "wp core install \
    --url=$DOCKER_IP \
    --title=my-site \
    --admin_user=admin \
    --admin_password=admin \
    --admin_email=admin@example.com \
&& wp plugin install wp-file-search \
&& wp plugin activate wp-file-search \
&& wp plugin install pdf-thumbnails \
&& wp plugin activate pdf-thumbnails \
&& wp plugin update akismet"
```

## Shutdown
- **$** `docker-compose down -v`

## Props
- https://docs.docker.com/compose/wordpress/#shutdown-and-cleanup
- https://www.anexia-it.com/blog/en/simplified-wordpress-development-with-docker-compose/
- https://www.michaelhaessig.com/2017/02/13/stateless-wordpress-docker-container/
- https://github.com/mbovel/docker-wordpress-autoinstall
- https://github.com/adambloomer/docker-compose--wordpress
- https://medium.com/@tatemz/using-wp-cli-with-docker-21b0ab9fab79
