FROM debian:bullseye-slim

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      git \
      build-essential \
      libusb-1.0-0-dev \
      librtlsdr0 \
      rtl-sdr \
      ca-certificates && \
    rm -rf /var/lib/apt/lists/*

RUN git clone --depth 1 https://github.com/flightaware/dump1090.git /src/dump1090 && \
    cd /src/dump1090 && \
    make

RUN cp /src/dump1090/dump1090 /usr/local/bin/

EXPOSE 8080 30005 30002

ENTRYPOINT ["/usr/local/bin/dump1090"]
CMD ["--net", "--gain", "max", "--device-index", "0"]
