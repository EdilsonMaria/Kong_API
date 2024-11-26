FROM golang:1.16 as build

WORKDIR /go/src

COPY . .
RUN GOOS=linux CGO_ENABLED=0 go build -o server main.go

EXPOSE 8080

CMD ["./main"]