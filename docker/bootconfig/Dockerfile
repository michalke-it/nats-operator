FROM golang:1.14-stretch AS builder
WORKDIR $GOPATH/src/github.com/nats-io/nats-operator/
RUN apt update && apt install git gcc
RUN go get -u github.com/golang/dep/cmd/dep
COPY . .
RUN dep ensure -v -vendor-only
RUN CGO_ENABLED=0 go build -o /nats-pod-bootconfig ./cmd/bootconfig/main.go

FROM alpine:3.8
COPY --from=builder /nats-pod-bootconfig /usr/local/bin/nats-pod-bootconfig
CMD ["nats-pod-bootconfig"]
