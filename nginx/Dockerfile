FROM debian:bookworm

RUN apt-get update && apt-get install -y \
    nginx \
    nano

ADD nginx.conf /etc/nginx/
COPY sites-available/* /etc/nginx/sites-available/

RUN rm -rf /etc/nginx/sites-enabled && ln -s /etc/nginx/sites-available /etc/nginx/sites-enabled

RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
