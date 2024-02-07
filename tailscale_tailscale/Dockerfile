FROM golang:alpine AS builder
WORKDIR /app

# https://tailscale.com/kb/1118/custom-derp-servers/
#RUN go env -w GOPROXY=https://goproxy.io,https://goproxy.cn,https://mirrors.aliyun.com/goproxy,direct
RUN go install tailscale.com/cmd/derper@main

FROM alpine
WORKDIR /app

ARG DEBIAN_FRONTEND=noninteractive

#RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories
RUN apk update && \
    apk add --no-cache ca-certificates && \
    rm -rf /var/cache/apk/* && \
    mkdir /app/certs

ENV DERP_DOMAIN your-hostname.com
ENV DERP_CERT_MODE letsencrypt
ENV DERP_CERT_DIR /app/certs
ENV DERP_ADDR :443
ENV DERP_STUN true
ENV DERP_STUN_PORT 3478
ENV DERP_HTTP_PORT 80
ENV DERP_VERIFY_CLIENTS false

COPY --from=builder /go/bin/derper .

CMD /app/derper --hostname=$DERP_DOMAIN \
    --certmode=$DERP_CERT_MODE \
    --certdir=$DERP_CERT_DIR \
    --a=$DERP_ADDR \
    --stun=$DERP_STUN  \
    --stun-port=$DERP_STUN_PORT \
    --http-port=$DERP_HTTP_PORT \
    --verify-clients=$DERP_VERIFY_CLIENTS
