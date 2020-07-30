FROM debian:jessie

RUN apt-get update && apt-get install -y \
    nginx \
    nano

ADD nginx.conf /etc/nginx/
COPY sites-available/* /etc/nginx/sites-available/

RUN ln -s /etc/nginx/sites-available/symfony.conf /etc/nginx/sites-enabled/symfony
RUN ln -s /etc/nginx/sites-available/cardy.conf /etc/nginx/sites-enabled/cardy
RUN echo "upstream php-upstream { server php:9000; }" > /etc/nginx/conf.d/upstream.conf

CMD ["nginx"]

EXPOSE 80
EXPOSE 443
