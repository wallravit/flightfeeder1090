FROM debian:bullseye-slim

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      wget \
      ca-certificates \
      libusb-1.0-0 \
      librtlsdr0 && \
    rm -rf /var/lib/apt/lists/*

RUN wget -O /tmp/fr24feed.tgz https://repo-feed.flightradar24.com/linux_armv7_binaries/fr24feed_1.0.46-0_armv7.tgz && \
    tar -xzf /tmp/fr24feed.tgz -C /usr/local/bin && \
    rm /tmp/fr24feed.tgz

WORKDIR /etc

ENTRYPOINT ["/usr/local/bin/fr24feed"]
CMD ["--no-web", "--config-file=/etc/fr24feed.ini"]
