FROM golang:1.15 as builder
WORKDIR /go/src/app
COPY . .
RUN export GOPROXY=https://goproxy.io,direct
RUN export GOSUMDB=off
RUN go get .
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM alpine:latest
WORKDIR /app
RUN apk --no-cache add ca-certificates
COPY --from=builder /go/src/app/app .
COPY --from=builder /go/src/app/seed.json .
EXPOSE 80
CMD ["./app"]
