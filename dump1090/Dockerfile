FROM debian:bullseye-slim

COPY dump1090-mutability_1.14_armhf.deb /tmp/dump1090-mutability_1.14_armhf.deb
RUN apt-get update && \
    apt-get install -y \
        rtl-sdr \
        wget \
        ca-certificates \
        libusb-1.0-0 \
        busybox \
        --no-install-recommends

RUN apt-get install -y /tmp/dump1090-mutability_1.14_armhf.deb && \
    rm /tmp/dump1090-mutability_1.14_armhf.deb

EXPOSE 8080 30005 30002

ENTRYPOINT ["/usr/bin/dump1090-mutability", "--net", "--interactive", "--gain", "max"]
