FROM node:18-alpine3.18
# Installing libvips-dev for sharp Compatibility
RUN apk update && apk add --no-cache build-base gcc autoconf automake zlib-dev libpng-dev nasm bash vips-dev git
ARG NODE_ENV=development
ENV NODE_ENV=${NODE_ENV}

WORKDIR /opt/
COPY package.json yarn.lock ./
RUN yarn global add node-gyp
RUN yarn config set network-timeout 600000 -g && yarn install
ENV PATH /opt/node_modules/.bin:$PATH

WORKDIR /opt/app

ARG HOST
ARG PORT
ARG APP_KEYS
ARG API_TOKEN_SALT
ARG ADMIN_JWT_SECRET
ARG TRANSFER_TOKEN_SALT
ARG JWT_SECRET
ARG DATABASE_CLIENT
ARG DATABASE_HOST
ARG DATABASE_PORT
ARG DATABASE_NAME
ARG DATABASE_PASSWORD
ARG DATABASE_SSL
ARG DATABASE_SSL_REJECT_UNAUTHORIZED
ARG DATABASE_USER


RUN touch .env
RUN echo "HOST=${HOST}" >> .env
RUN echo "PORT=${PORT}" >> .env
RUN echo "APP_KEYS=${APP_KEYS}" >> .env
RUN echo "API_TOKEN_SALT=${API_TOKEN_SALT}" >> .env
RUN echo "ADMIN_JWT_SECRET=${ADMIN_JWT_SECRET}" >> .env
RUN echo "TRANSFER_TOKEN_SALT=${TRANSFER_TOKEN_SALT}" >> .env
RUN echo "DATABASE_CLIENT=${DATABASE_CLIENT}" >> .env
RUN echo "DATABASE_USER=${DATABASE_USER}" >> .env
RUN echo "JWT_SECRET=${JWT_SECRET}" >> .env
RUN echo "NODE_ENV=${NODE_ENV}" >> .env
RUN echo "PORT=${PORT}" >> .env
RUN echo "DATABASE_HOST=${DATABASE_HOST}" >> .env
RUN echo "DATABASE_NAME=${DATABASE_NAME}" >> .env
RUN echo "DATABASE_PASSWORD=${DATABASE_PASSWORD}" >> .env
RUN echo "DATABASE_PORT=${DATABASE_PORT}" >> .env
RUN echo "DATABASE_SSL=${DATABASE_SSL}" >> .env
RUN echo "DATABASE_SCHEMA=${DATABASE_SCHEMA}" >> .env
RUN echo "DATABASE_SSL_REJECT_UNAUTHORIZED=${DATABASE_SSL_REJECT_UNAUTHORIZED}" >> .env

COPY . .
RUN chown -R node:node /opt/app
USER node
RUN ["yarn", "build"]
EXPOSE 1337
CMD ["yarn", "dev"]