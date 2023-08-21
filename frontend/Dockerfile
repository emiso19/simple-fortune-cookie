#######################
####    Builder    ####
#######################

FROM golang:1.21 as builder

WORKDIR /frontend

COPY go.mod ./

RUN go mod download

COPY ./ ./

RUN CGO_ENABLED=0 go build -o frontend

#######################
####  Application  ####
#######################

FROM alpine:latest

WORKDIR /root/

RUN apk --no-cache add ca-certificates

COPY --from=builder /frontend/frontend .
COPY --from=builder /frontend/static static
COPY --from=builder /frontend/templates templates

EXPOSE 8080

CMD ["/root/frontend"]
