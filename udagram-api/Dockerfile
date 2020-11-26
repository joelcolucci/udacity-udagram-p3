FROM node:12-alpine

WORKDIR /app

COPY package.json ./

RUN apk --no-cache --virtual build-dependencies add \
    python \
    make \
    g++ \
    && npm install \
    && apk del build-dependencies

COPY . .

RUN npm run tsc

CMD ["node", "www/server.js"]