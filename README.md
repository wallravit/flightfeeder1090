# ADS-B Docker Feeder

A complete Docker Compose setup for running [dump1090](https://github.com/mutability/dump1090) and [FR24feed](https://www.flightradar24.com/share-your-data) using an SDR-RTL USB dongle.
**Tested on Raspberry Pi 4 (ARM/ARM64), but works on other Linux devices too!**

---

## Features

* **dump1090**: Decodes ADS-B data from aircraft with your SDR-RTL dongle.
* **FR24feed**: Shares your data with Flightradar24.

---

## Project Structure

```
.
├── docker-compose.yml
├── fr24feed/
│   └── Dockerfile
├── dump1090/
│   └── Dockerfile
└── fr24feed.ini
```

---

## Getting Started

### 1. Prerequisites

* Docker & Docker Compose installed
* SDR-RTL USB dongle connected
* Raspberry Pi OS (32- or 64-bit) or similar Linux system

### 2. Setup

#### a) Clone this repository

```sh
git clone https://github.com/wallravit/flightfeeder1090
cd flightfeeder1090
```

#### b) Get your Flightradar24 sharing key and generate `fr24feed.ini`

* Run the FR24feed wizard on any machine to get your config, or use the sample below.
* Place your `fr24feed.ini` in the project root (same folder as `docker-compose.yml`).

#### c) Build and launch

```sh
docker compose up -d
```

---

## Usage

* **dump1090 web UI**: [http://localhost:8080](http://localhost:8080)
* **FR24feed stats**: Check your dashboard at [Flightradar24](https://www.flightradar24.com/account/feed-stats/)

---

## Configuration

* **Edit `fr24feed.ini`** with your sharing key and settings.
* **Change dump1090 parameters** by editing `command:` in `docker-compose.yml`.

---

## Example `fr24feed.ini`

```ini
receiver="beast-tcp"
fr24key="YOUR_SHARING_KEY_HERE"
host="dump1090:30005"
bs="no"
raw="no"
logmode="1"
mlat="yes"
mlat-without-gps="yes"
```

---

## Troubleshooting

* **SDR dongle not detected:**
  Make sure `/dev/bus/usb` is mapped in the compose file and your user has access to USB devices.
* **No data to FR24:**
  Check your `fr24feed.ini` and make sure the host matches the `dump1090` service and port.

