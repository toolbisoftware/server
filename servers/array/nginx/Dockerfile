FROM ubuntu:latest

# Update the package repository
RUN apt-get update -y

# Setup NGINX
RUN apt-get install -y nginx
WORKDIR /etc/nginx
RUN rm nginx.conf
RUN rm ./sites-enabled/default
COPY ./files/nginx.conf nginx.conf
COPY ./files/sites-enabled/* ./sites-enabled/

# Setup the external certificates
WORKDIR /
RUN mkdir -p external
WORKDIR /external
RUN mkdir -p certificates/domains \
  && mkdir -p certificates/mailcow \
  && mkdir -p certificates/pterodactyl
VOLUME /external/certificates/domains
VOLUME /external/certificates/mailcow
VOLUME /external/certificates/pterodactyl

# Clean up
RUN rm -rf /var/lib/apt/lists/*

# Setup entrypoint
COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT /entrypoint.sh

# Expose the ports
EXPOSE 80
EXPOSE 443
