FROM debian:bullseye-slim

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
      build-essential \
      pkg-config \
      libusb-1.0-0-dev \
      librtlsdr0 \
      rtl-sdr && \
    rm -rf /var/lib/apt/lists/*

COPY dump1090-1.14 /src/dump1090

RUN cd /src/dump1090 && make
RUN cp /src/dump1090/dump1090 /usr/local/bin/

EXPOSE 8080 30005 30002

ENTRYPOINT ["/usr/local/bin/dump1090"]
CMD ["--net", "--gain", "max", "--device-index", "0"]
