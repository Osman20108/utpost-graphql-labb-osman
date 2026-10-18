# Steg 1: bygg Vue-appen med Node
FROM node:22-alpine AS build

WORKDIR /app

COPY package.json package-lock.json ./
COPY shared/package.json shared/
COPY client/package.json client/

RUN npm ci --workspace=client

COPY shared/ shared/
COPY client/ client/

RUN npm run build --workspace=client


# Steg 2: kör endast den färdigbyggda appen med nginx
FROM nginx:1.27-alpine
COPY client/nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=build /app/client/dist /usr/share/nginx/html

EXPOSE 80