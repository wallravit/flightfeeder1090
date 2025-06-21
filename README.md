# ADS-B Docker Feeder

A plug-and-play Docker Compose setup for running [dump1090](https://github.com/mutability/dump1090) and [FR24feed](https://www.flightradar24.com/share-your-data) with an SDR-RTL USB dongle.

**Tested on Raspberry Pi 4 (ARM/ARM64), but works on most Linux systems!**

---

## Features

* **dump1090:** Decodes ADS-B signals from aircraft using your SDR-RTL dongle.
* **FR24feed:** Forwards your data to Flightradar24 for community sharing.

---

## Getting Started

### 1. Prerequisites

* Docker & Docker Compose installed
* SDR-RTL USB dongle connected
* Raspberry Pi OS (32- or 64-bit) or compatible Linux distro
* `udev` installed

### 2. Setup Instructions

#### a) Clone the repository

```sh
git clone https://github.com/wallravit/flightfeeder1090
cd flightfeeder1090
```

#### b) Configure udev for rootless SDR-RTL access

1. Install udev (if not already):

   ```sh
   sudo apt install udev
   ```
2. Copy the udev rule:

   ```sh
   sudo cp dump1090/rules.d/10-rtl-sdr.rules /etc/udev/rules.d/
   ```
3. Reload udev rules and trigger:

   ```sh
   sudo udevadm control --reload-rules && sudo udevadm trigger
   ```
4. Reboot your system.

#### c) Obtain your Flightradar24 sharing key and create `fr24feed.ini`

* Run the FR24feed wizard on any machine to generate your config, or use the sample below.
* Place your `fr24feed.ini` file in the project root (same directory as `docker-compose.yml`).

#### d) Build and launch the services

```sh
docker compose up -d
```

---

## Usage

* **dump1090 web UI:** [http://localhost:8080](http://localhost:8080)
* **FR24feed stats:** View your dashboard on [Flightradar24](https://www.flightradar24.com/account/feed-stats/)

---

## Configuration

* **fr24feed.ini:** Edit your sharing key and other settings.
* **dump1090 parameters:** Modify the `command:` section in `docker-compose.yml` to change options.

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
  Ensure `/dev/bus/usb` is mapped in the Compose file and your user has permission to access USB devices.
* **No data sent to FR24:**
  Double-check your `fr24feed.ini` configuration, especially that `host` matches the dump1090 service and port.

