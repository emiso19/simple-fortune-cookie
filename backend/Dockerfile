#######################
####    Builder    ####
#######################

FROM golang:1.21 as builder

WORKDIR /backend

COPY go.mod go.sum ./

RUN go mod download

COPY ./ ./

RUN go build -o backend

#######################
####  Application  ####
#######################

FROM alpine:latest

WORKDIR /root/

RUN apk --no-cache add ca-certificates

COPY --from=builder /backend/backend .

EXPOSE 9000

CMD ["./backend"]
