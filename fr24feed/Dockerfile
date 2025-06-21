FROM debian:bullseye-slim

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      ca-certificates \
      libusb-1.0-0 \
      librtlsdr0 && \
    rm -rf /var/lib/apt/lists/*

COPY fr24feed_armhf /usr/local/bin/fr24feed

RUN chmod +x /usr/local/bin/fr24feed

WORKDIR /etc

ENTRYPOINT ["/usr/local/bin/fr24feed"]
CMD ["--no-web", "--config-file=/etc/fr24feed.ini"]
