FROM node:14 AS build-phase

WORKDIR /usr/src/app

COPY . .

RUN npm install -g serve && \
    npm install && \
    npm run build

FROM node:14-alpine3.13

EXPOSE 5000

WORKDIR /usr/src/app

COPY --from=build-phase /usr/src/app/build/ /usr/src/app/build

RUN npm install -g serve && \
    adduser -D appuser && \
    chown appuser build

USER appuser

ENTRYPOINT [ "serve", "-s", "-l", "5000", "build" ]

