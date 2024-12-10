FROM golang:1.20 AS builder

WORKDIR /app
COPY dispatcher.go .       
COPY static ./static       

# Compilation statique pour compatibilité avec Alpine
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o dispatcher dispatcher.go

FROM alpine:3.18

WORKDIR /app
COPY --from=builder /app/dispatcher .
COPY --from=builder /app/static ./static

EXPOSE 80
CMD ["./dispatcher"]

