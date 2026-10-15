FROM node:16-alpine AS build

WORKDIR /usr/local/app
# Dependances d'abord : couche mise en cache tant que package*.json ne change pas
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:stable-alpine AS production

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /usr/local/app/dist/bobapp /usr/share/nginx/html

EXPOSE 80
