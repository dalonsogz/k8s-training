FROM golang:1.15-alpine as builder
WORKDIR /tmp
RUN apk add git upx --no-cache && \
    go get github.com/pwaller/goupx
COPY demo-app.go /tmp
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o demo-app -ldflags="-s -w" . && \
    goupx demo-app

FROM alpine:latest
RUN apk add curl libcap --no-cache
COPY --from=builder /tmp/demo-app /demo-app
EXPOSE 8080
CMD ["./demo-app"]

# more info
# https://docs.docker.com/develop/develop-images/multistage-build/
# https://blog.filippo.io/shrink-your-go-binaries-with-this-one-weird-trick/
