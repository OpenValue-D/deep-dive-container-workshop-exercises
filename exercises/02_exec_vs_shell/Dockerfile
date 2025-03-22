FROM golang:1.20 AS builder

ARG TARGETOS
ARG TARGETARCH

WORKDIR /app
COPY main.go .
RUN CGO_ENABLED=0 GOOS=${TARGETOS} GOARCH=${TARGETARCH} go build -ldflags="-s -w" -o app main.go

FROM debian:trixie-slim
RUN apt-get update && apt-get install -y --no-install-recommends procps && rm -rf /var/lib/apt/lists/*
COPY --from=builder /app/app /
EXPOSE 8080
CMD /app