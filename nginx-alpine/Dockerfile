FROM alpine:latest

MAINTAINER anakinpendragon - anakinpendragon@gmail.com 

ENV NGINX_VERSION nginx-1.20.1
ENV OPENSSL_VERSION openssl-1.1.1k

RUN apk --update add pcre-dev zlib-dev wget build-base geoip-dev git perl-dev linux-headers && \
mkdir -p /tmp/src && \
mkdir -p /tmp/uwsgi && \
cd /tmp/src && \
wget http://nginx.org/download/${NGINX_VERSION}.tar.gz && \
tar -zxvf ${NGINX_VERSION}.tar.gz && \
wget https://www.openssl.org/source/${OPENSSL_VERSION}.tar.gz && \
tar -zxvf ${OPENSSL_VERSION}.tar.gz && \
git clone --recursive https://github.com/google/ngx_brotli.git /tmp/src/brotli && \
git clone https://github.com/vozlt/nginx-module-vts.git /tmp/src/vts && \
cd /tmp/src/${NGINX_VERSION} && \
./configure \
--with-http_ssl_module \
--with-http_gzip_static_module \
--with-openssl=/tmp/src/${OPENSSL_VERSION}/ \
--add-module=/tmp/src/brotli \
--add-module=/tmp/src/vts \
--with-http_v2_module \
--with-http_geoip_module \
--with-pcre-jit \
--with-http_realip_module \
--http-uwsgi-temp-path=/tmp/uwsgi \
--prefix=/usr/share/nginx \
--sbin-path=/usr/sbin/nginx \
--modules-path=/usr/lib64/nginx/modules \
--conf-path=/etc/nginx/nginx.conf \
--error-log-path=/var/log/nginx/error.log \
--http-log-path=/var/log/nginx/access.log \
--http-log-path=/var/log/nginx/access.log \
--error-log-path=/var/log/nginx/error.log \
--sbin-path=/usr/local/sbin/nginx && \
make && \
make install && \
apk del build-base git linux-headers git perl-dev wget && \
mkdir /etc/nginx/conf.d && \
apk del pcre-dev zlib-dev wget build-base geoip-dev git perl-dev linux-headers && \
apk add pcre geoip && \
rm -rf /tmp/src && \
rm -rf /var/cache/apk/* && \ 
# forward request and error logs to docker log collector
    ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/log/nginx"]

WORKDIR /etc/nginx
#COPY nginx.conf /etc/nginx
EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"] 
