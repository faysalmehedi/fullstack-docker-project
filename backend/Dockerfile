FROM golang:1.16 AS build-env

WORKDIR /usr/src/app

COPY . .

ENV CGO_ENABLED=0
RUN go build && \
    useradd -m appuser && \
    chown appuser server

FROM scratch

EXPOSE 8080

WORKDIR /usr/src/app

COPY --from=build-env /usr/src/app/server /usr/src/app
COPY --from=build-env /etc/passwd /etc/passwd

USER appuser

ENTRYPOINT [ "./server" ]