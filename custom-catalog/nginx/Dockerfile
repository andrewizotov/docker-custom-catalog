FROM nginx:1.11

COPY default.conf /etc/nginx/conf.d/default.conf
#RUN apt-get update && apt-get install -y vim 
RUN echo "www-data ALL = NOPASSWD: ALL" >> /etc/sudoers
VOLUME /etc/nginx
VOLUME /var/log/nginx/log
WORKDIR /var/www/html/application
USER root
