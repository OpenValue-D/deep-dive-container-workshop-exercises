FROM golang:1.20 AS builder

ARG TARGETOS
ARG TARGETARCH

WORKDIR /app

COPY hello.go .

RUN CGO_ENABLED=0 GOOS=${TARGETOS} GOARCH=${TARGETARCH} go build -ldflags="-s -w" hello.go

FROM debian:trixie-slim

COPY --from=builder /app/hello .

CMD ["./hello"]