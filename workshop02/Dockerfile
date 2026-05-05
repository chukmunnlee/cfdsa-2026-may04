FROM node:25-bookworm AS builder

WORKDIR /src

# copy the Angular application into the container
COPY *.json .
COPY src src
COPY public public

# Install the Angular CLI, install dependecies, build Angular
# The files will be in dist/countingbook/browser/*
RUN npm install -g @angular/cli && npm ci && ng build

FROM caddy:2-alpine

WORKDIR /app

# Create html directory
RUN mkdir html

COPY --from=builder /src/dist/countingbook/browser/ html
COPY caddy/error.html html
COPY caddy/Caddyfile .

ENV CADDY_PORT=3000

ENTRYPOINT caddy run --config Caddyfile
