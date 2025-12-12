# Builder stage
FROM registry.access.redhat.com/ubi10/go-toolset:10.0 AS builder


USER 0
WORKDIR /opt/app-root/src

COPY go.mod ./
COPY main.go ./

RUN go mod tidy
RUN go build -o guestbook-api .

FROM registry.access.redhat.com/ubi10-minimal:10.0

WORKDIR /opt/app-root/src
COPY --from=builder /opt/app-root/src/guestbook-api /opt/app-root/src/guestbook-api

EXPOSE 8080
ENV PORT=8080

CMD ["/opt/app-root/src/guestbook-api"]
