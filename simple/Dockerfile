FROM nginx

RUN apt-get update
RUN apt-get install -qq curl

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 8.4.0

RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz"

RUN tar -zxvf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
    && rm "node-v$NODE_VERSION-linux-x64.tar.gz" \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs

RUN npm install -g create-react-app

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ARG NODE_ENV
ENV NODE_ENV $NODE_ENV
RUN rm -rf build || true
ONBUILD COPY ./package.json /usr/src/app
ONBUILD RUN npm install

ONBUILD COPY ./public /usr/src/app/public
ONBUILD COPY ./src /usr/src/app/src
ONBUILD RUN npm run build

ONBUILD RUN rm -rf /usr/share/nginx/html/* || true
ONBUILD RUN chmod -R 777 ./build/*
ONBUILD RUN cp -r ./build/* /usr/share/nginx/html/

COPY ./nginx.conf /etc/nginx/nginx.conf
