FROM golang:1.5

RUN apt-get update && apt-get install -y --no-install-recommends \
		unzip \
	&& rm -rf /var/lib/apt/lists/*

RUN mkdir -p /go/src/github.com/shadowsocks
WORKDIR /go/src/github.com/shadowsocks

COPY shadowsocks-server-wrapper /usr/local/bin/
RUN chmod a+x /usr/local/bin/shadowsocks-server-wrapper

#ENV GOROOT /usr/local/go/

ENV SHADOWSOCKS_VERSION 1.1.4
ENV SHADOWSOCKS_DOWNLOAD_URL https://github.com/shadowsocks/shadowsocks-go/archive/$SHADOWSOCKS_VERSION.zip
#ENV SHADOWSOCKS_DOWNLOAD_SHA1 cae87ed095e8d94a81871281d35da7829bd1234e

RUN curl -fsSL "$SHADOWSOCKS_DOWNLOAD_URL" -o shadowsocks-go.zip \
	&& unzip shadowsocks-go.zip \
	&& rm shadowsocks-go.zip \
	&& mv shadowsocks-go-$SHADOWSOCKS_VERSION shadowsocks-go

RUN go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server


CMD ["shadowsocks-server-wrapper"]
