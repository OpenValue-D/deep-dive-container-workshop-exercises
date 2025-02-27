FROM ubuntu

LABEL owner="openvalue"

ARG TARGETOS
ARG TARGETARCH

RUN apt-get update
RUN apt install -y golang-go

ADD hello.go .
ADD license.txt .

RUN CGO_ENABLED=0 GOOS=${TARGETOS} GOARCH=${TARGETARCH} go build -ldflags="-s -w" hello.go

CMD ./hello