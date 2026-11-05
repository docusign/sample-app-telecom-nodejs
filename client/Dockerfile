FROM --platform=linux/amd64 node:26.12.1 AS development

WORKDIR /usr/src/app

COPY package.json package.json
COPY .npmrc .npmrc
COPY package-lock.json package-lock.json

RUN npm install
COPY . .
RUN npm run build

FROM --platform=linux/amd64 nginx:1.27-alpine

COPY --from=development /usr/src/app/build /usr/share/nginx/html
COPY nginx/conf/default.conf /etc/nginx/conf.d/
