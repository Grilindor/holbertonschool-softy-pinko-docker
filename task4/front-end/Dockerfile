# update to the latest version of all packages
FROM nginx:latest
# copied all files in softy-pinko-front-end on the Docker image
COPY ./softy-pinko-front-end /var/www/html/softy-pinko-front-end

# copy custom nginx config to appropriate location
COPY ./softy-pinko-front-end.conf /etc/nginx/conf.d/default.conf
