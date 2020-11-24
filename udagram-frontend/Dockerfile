FROM node:12-alpine as build

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY ./ /app/

RUN npm run build

FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*

COPY --from=build /app/www/ /usr/share/nginx/html/