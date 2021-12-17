FROM node:12.22.7-alpine AS builder
#FROM ros:melodic-ros-core-bionic

RUN apk update && \
    apk add --no-cache \
    git && \
    rm -rf /var/cache/apk/*

# clone sourcecode
RUN git clone https://github.com/georgealexakis/ros-joystick.git /app

WORKDIR /app

RUN npm install && \
    ln -s desktop.html index.html

# start new samller container
FROM nginx:1-alpine

LABEL maintainer="Waipot Ngamsaad <waipotn@hotmail.com>"

RUN sed -i 's/listen  *80;/listen 8080;/g' /etc/nginx/conf.d/default.conf

EXPOSE 8080

COPY --from=builder /app /usr/share/nginx/html
