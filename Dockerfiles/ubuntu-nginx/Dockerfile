# Image base
FROM ubuntu:14.04
# Author
MAINTAINER Didier Youn <didier.youn@gmail.com>
# Create user and group
RUN groupadd -r www-user \
    && useradd -r -g www-user www-user
# Set user and group permissions
RUN mkdir -p /data/www \ 
    && chown -R www-user:www-user /data/www
# Update & install package
RUN apt-get update \
    && apt-get install -y software-properties-common \
    && apt-add-repository -y ppa:nginx/stable \
    && apt-get update \
    && apt-get install -y nginx \
    && rm -rf /var/lib/apt/lists/*
# Change nginx configurations 
ADD ./conf/nginx.conf /etc/nginx/nginx.conf
ADD ./conf/default.conf /etc/nginx/conf.d/default.conf
# Workdir 
ADD app/ /data/www
ADD app/ /var/www/html
# Delete nginx folder (unused)
RUN rm /etc/nginx/sites-enabled/default
# Create symlink for nginx logs
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log
# Work directory
VOLUME /data/www
WORKDIR /data/www
# Expose ports
EXPOSE 80 443
# User
# USER didier
# Run nginx
CMD ["nginx", "-g", "daemon off;"]