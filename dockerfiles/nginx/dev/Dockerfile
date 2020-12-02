FROM debian:buster-slim

ARG DOCKER_ENV
ARG SERVER_DOMAIN
ARG SERVER_PORT

# Install nginx, openssl
RUN apt-get update && apt-get install -y nginx \
    openssl \
    nano

# Add certs
RUN mkdir /certs
COPY dockerfiles/nginx/${DOCKER_ENV}/certs/ /certs/

# Configure nginx
COPY dockerfiles/nginx/${DOCKER_ENV}/config/default.conf /etc/nginx/
COPY dockerfiles/nginx/${DOCKER_ENV}/config/nginx.conf /etc/nginx/
COPY dockerfiles/nginx/${DOCKER_ENV}/config/admin_${DOCKER_ENV}.conf /etc/nginx/sites-available/
RUN sed -i "s|{{SERVER_DOMAIN}}|${SERVER_DOMAIN}|g" /etc/nginx/sites-available/admin_${DOCKER_ENV}.conf
RUN sed -i "s|{{SERVER_PORT}}|${SERVER_PORT}|g" /etc/nginx/sites-available/admin_${DOCKER_ENV}.conf
COPY dockerfiles/nginx/${DOCKER_ENV}/config/api_${DOCKER_ENV}.conf /etc/nginx/sites-available/
RUN   sed -i "s|{{SERVER_DOMAIN}}|${SERVER_DOMAIN}|g" /etc/nginx/sites-available/api_${DOCKER_ENV}.conf
RUN   sed -i "s|{{SERVER_PORT}}|${SERVER_PORT}|g" /etc/nginx/sites-available/api_${DOCKER_ENV}.conf
RUN usermod -u 1000 www-data



# Configure the virtual host
RUN ln -s /etc/nginx/sites-available/admin_${DOCKER_ENV}.conf /etc/nginx/sites-enabled/admin_${DOCKER_ENV}; \
    ln -s /etc/nginx/sites-available/api_${DOCKER_ENV}.conf /etc/nginx/sites-enabled/api_${DOCKER_ENV}; \
    rm /etc/nginx/sites-enabled/default

CMD ["nginx"]

WORKDIR /etc/nginx/sites-available

EXPOSE 80
EXPOSE 443
