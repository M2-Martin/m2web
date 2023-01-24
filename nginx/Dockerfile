ARG baseimage

FROM $baseimage

ARG domain

COPY ./acme.conf /etc/nginx/scripts/acme.conf
COPY ./ssl-common.conf /etc/nginx/scripts/ssl-common.conf
COPY ./dhparam.pem /etc/nginx/dhparam.pem

RUN openssl req -x509 -nodes -days 365 -subj "/C=CA/ST=QC/O=Company, Inc./CN=mydomain.com" -addext "subjectAltName=DNS:mydomain.com" -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt

RUN echo 'limit_conn_zone $binary_remote_addr zone=perip:10m;' >> /etc/nginx/conf.d/nginx-usr.conf
COPY ./default.conf /etc/nginx/conf.d/default.conf
COPY ./global.conf /etc/nginx/scripts/global.conf
RUN sed -i "s/DOMAIN/$domain/g" /etc/nginx/conf.d/default.conf
