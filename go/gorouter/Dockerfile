FROM golang:1.12 AS buildenv

ENV GO111MODULE=on
ENV CGO_ENABLED=0
ENV GOOS=linux
ENV GOARCH=amd64
ENV GOPROXY=https://proxy.golang.org

WORKDIR /go/src/app
ADD main.go go.mod ./

RUN go get
RUN go build -a -ldflags '-extldflags "-static"' -o /go/bin/app ./

FROM alpine:3.10
COPY --from=buildenv /go/bin/app /go/bin/app
CMD ["/go/bin/app"]
