# what is the base image ?? node:25-bookworm
ARG NODE_VER=25-bookworm
FROM node:${NODE_VER}

# Create a directory /app for coping my src
# mkdir /app
# cd /app
WORKDIR /app

# Inside /app
# copy files
COPY *.json .
COPY main.js .
# copy directories
COPY public  public
COPY views views

# Install dependencies
RUN npm i

## How to run

ENV APP_PORT=3000

EXPOSE ${APP_PORT}

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
   CMD curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1

# shell form
ENTRYPOINT node /app/main.js
