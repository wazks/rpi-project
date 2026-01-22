# RPI Broker (Mosquitto)

This broker accepts MQTT messages from multiple Raspberry Pi sensors and
provides them to the Django backend for storage and to any frontend clients
for real-time display.

## Raspberry Pi setup

These steps assume Raspberry Pi OS (Debian-based) and a user with sudo.

### Install prerequisites

```bash
sudo apt-get update
sudo apt-get install -y git ca-certificates curl

# Docker Engine + Compose plugin
curl -fsSL https://get.docker.com | sudo sh
sudo usermod -aG docker $USER
sudo systemctl enable --now docker
```

Log out and log back in so the docker group change takes effect.

### Clone and configure

```bash
git clone <your-repo-url> rpi-broker
cd rpi-broker
```

If you need to edit broker settings, update `config/mosquitto.conf`.

## Start the broker

```bash
docker compose up -d
```

Verify:

```bash
docker compose ps
```

## Test publish/subscribe

In one terminal:

```bash
docker exec -it rpi-mosquitto mosquitto_sub -t rpi/temperature
```

In another:

```bash
docker exec -it rpi-mosquitto mosquitto_pub -t rpi/temperature -m "23.6"
```

## Ports

- `1883` MQTT
- `9001` WebSocket MQTT (optional)
