### STAGE1:build angular application ###
FROM node:8 AS builder

COPY testapp /testapp

WORKDIR  /testapp

RUN npm install

RUN $(npm bin)/ng build

### STAGE2: RUN nginx to serve application ###
FROM nginx

COPY --from=builder /testapp/dist /* /usr/share/nginx/html

EXPOSE 80
