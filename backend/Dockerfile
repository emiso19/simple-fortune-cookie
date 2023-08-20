#######################
####    Builder    ####
#######################

FROM golang:1.21 as builder

WORKDIR /backend

COPY go.mod go.sum ./

RUN go mod download

COPY ./ ./

RUN CGO_ENABLED=0 go build -o backend

#######################
####  Application  ####
#######################

FROM alpine:latest

WORKDIR /root/

COPY --from=builder /backend/backend .

EXPOSE 9000

CMD ["/root/backend"]
