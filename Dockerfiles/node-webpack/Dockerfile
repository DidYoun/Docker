FROM node:latest

MAINTAINER Didier Youn "didier.youn@gmail.com"

RUN apt-get update -qq
RUN npm install webpack -g

WORKDIR /tmp

COPY package.json /tmp/
RUN npm config set registry http://registry.npmjs.org/ && npm install

WORKDIR /usr/src/app
COPY . /usr/src/app/

RUN cp -a /tmp/node_modules /usr/src/app/
RUN webpack

ENV NODE_ENV=production
ENV PORT=4000

EXPOSE 4000

CMD ["/usr/local/bin/node", "./index.js"]