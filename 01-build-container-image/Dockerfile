# syntax=docker/dockerfile:1

FROM golang:1.24-alpine AS build

ARG TARGETOS=linux
ARG TARGETARCH=arm64
ENV GOOS=${TARGETOS}
ENV GOARCH=${TARGETARCH}

WORKDIR /build
RUN apk add --no-cache git

# Clone a specific version of go2rtc
RUN git clone --depth 1 -b v1.9.14 https://github.com/AlexxIT/go2rtc.git .

# Download dependencies and build
RUN go mod download
RUN CGO_ENABLED=0 go build -ldflags "-s -w" -trimpath -o /usr/local/bin/go2rtc

# -------------------------
# Final runtime image
FROM python:3.13-alpine

# Install essential dependencies for go2rtc
RUN apk add --no-cache \
    tini \
    ffmpeg \
    bash \
    curl \
    jq

# Copy the built binary
COPY --from=build /usr/local/bin/go2rtc /usr/local/bin/go2rtc

# Expose ports:
# 1984: Web UI / API
# 8554: RTSP
# 8555: WebRTC (TCP & UDP)
EXPOSE 1984 8554 8555 8555/udp

ENTRYPOINT ["/sbin/tini", "--"]

VOLUME /config
WORKDIR /config

# Ensure a default config file exists or will be provided, then start
CMD ["go2rtc", "-config", "/config/go2rtc.yaml"]
