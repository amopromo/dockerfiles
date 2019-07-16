#Dockerfile para criar worker novo em python 
#Cria primeiro uma imagem com python e suas dependencias 
#Exemplo de comando:
#Compilacao do python 3.7.3 que o projeto exige
FROM alpine:latest

# Update & Install dependencies
RUN apk add --no-cache --update \
    git \
    bash \
    libffi-dev \
    openssl-dev \
    bzip2-dev \
    zlib-dev \
    readline-dev \
    sqlite-dev \
    build-base \
    linux-headers \
    postgresql-dev \
    libxml2-dev \
    libxslt-dev


# Set Python version
ARG PYTHON_VERSION='3.7.4'
# Set pyenv home
ARG PYENV_HOME=/root/.pyenv

# Install pyenv, then install python versions
RUN git clone --depth 1 https://github.com/pyenv/pyenv.git $PYENV_HOME && \
    rm -rfv $PYENV_HOME/.git

ENV PATH $PYENV_HOME/shims:$PYENV_HOME/bin:$PATH

RUN pyenv install $PYTHON_VERSION
RUN pyenv global $PYTHON_VERSION
RUN pip install --upgrade pip && pyenv rehash

# Clean
RUN rm -rf ~/.cache/pip

#########################################################

RUN pip install uwsgi
RUN apk --no-cache add ca-certificates

WORKDIR /usr/src/passagenspromo/src 
