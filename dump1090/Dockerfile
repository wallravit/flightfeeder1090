FROM debian:bullseye-slim

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    dump1090-mutability \
    --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 8080 30001 30002 30003 30004 30005 30104

CMD ["dump1090-mutability", "--net", "--net-http-port", "8080"]