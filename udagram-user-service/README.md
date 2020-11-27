# Project 3
1. DONE Create docker for udagram API
2. DONE Create docker-compose for udagram API + postgrs
3. Factor out /feeds from /users -> docker-compose into separate repos
4. Create docker for udagram client
5. Setup CI
6. Setup orchestration





1. Get app running on a local docker container
2. Get app running in a pod with distinct database
3. Deploy as one

THEN
1. Split up into two



FROM node:12

WORKDIR /app

COPY package.json ./

RUN npm install && npm run build

COPY . .

CMD ["node", "www/server.js"]



ENV PM2_PUBLIC_KEY <Public key>
ENV PM2_SECRET_KEY <Secret Key>
ENV NODE_ENV production
ENV MONGO_URL <Mongo url>
ENV PORT 3000



docker run -d \
    --network todo-app --network-alias mysql \
    -v todo-mysql-data:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=secret \
    -e MYSQL_DATABASE=todos \
    mysql:5.7

docker run -dp 8100:8100 udagram-api \
  -e POSTGRES_USERNAME=vagrant \
  -e POSTGRES_PASSWORD=vagrant \
  -e POSTGRES_HOST=localhost \
  -e POSTGRES_DB=udagramfeeds \
  -e AWS_BUCKET=udagram-feeds-service \
  -e AWS_REGION=us-east-1 \
  -e AWS_PROFILE=default \
  -e JWT_SECRET=iamsupersecret \
  -e URL=http://localhost:8100 \
  -e PORT=8100 
























version: "3.7"

services:
  app:
    image: node:12-alpine
    command: sh -c "yarn install && yarn run dev"
    ports:
      - 3000:3000
    working_dir: /app
    volumes:
      - ./:/app
    environment:
      MYSQL_HOST: mysql
      MYSQL_USER: root
      MYSQL_PASSWORD: secret
      MYSQL_DB: todos

  mysql:
    image: mysql:5.7
    volumes:
      - todo-mysql-data:/var/lib/mysql
    environment: 
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: todos

volumes:
  todo-mysql-data:





  WARNING: Image for service app was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.