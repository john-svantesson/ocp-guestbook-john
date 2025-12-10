FROM registry.access.redhat.com/ubi10/go-toolset:10.0 AS builder
USER root

WORKDIR /opt/app-root/src


COPY go.mod ./
RUN go mod tidy
RUN go mod download


COPY main.go .
RUN go build -o guestbook-api .


FROM registry.access.redhat.com/ubi10-minimal:10.0
WORKDIR /
COPY --from=builder /opt/app-root/src/guestbook-api /guestbook-api
EXPOSE 8080
CMD ["/guestbook-api"]
