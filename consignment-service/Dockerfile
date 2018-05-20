FROM golang:1.9.0 as builder

WORKDIR /go/src/github.com/zzayne/shipper/consignment-service

COPY .  .
RUN export http_proxy=duotai:pRPfSOcntV@hilton.h.timonit.cn:18102
RUN export https_proxy=$http_proxy
RUN go get -u github.com/golang/dep/cmd/dep

RUN dep init && dep ensure

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo .


FROM debian:latest

RUN apk --no-cache add ca-certificates

RUN mkdir /app
WORKDIR /app

COPY --from=builder /go/src/github.com/zzayne/shipper/consignment-service/consignment-service .

CMD ["./consignment-service"]