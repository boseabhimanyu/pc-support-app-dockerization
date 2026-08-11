FROM golang:1.25 AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o server ./cmd/main.go


FROM alpine:3.22

WORKDIR /app

COPY --from=builder /app/server .

EXPOSE 6543

CMD ["./server"]