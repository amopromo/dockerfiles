FROM amopromo/python3.7-nginx:latest 
ENV LANG C.UTF-8

# Dependencias para compilacao 
RUN     apk add --no-cache --virtual .fetch-deps \
        libxml2-dev \
        libxslt-dev \
        git \
        go \
        make \
        build-base \
        linux-headers \ 
        npm && \
# Baixa codigo e compila
    cd /usr/src/ && \
    git clone https://github.com/nginx/unit && \
    cd /usr/src/unit/  && \
    ./configure --state=/var/lib/unit --log=/var/log/unit.log \
              --control=unix:/run/control.unit.sock --prefix=/usr/local/  && \
    make install && \
    ./configure python  && \
    make install && \
# Remove pacotes que nao sao mais necessarios
    apk add curl && \
    apk del git \
    go \
    make \
    build-base \
    linux-headers \
    .fetch-deps && \
    rm -Rf /usr/src/unit


CMD ["unitd"]

