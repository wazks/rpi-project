# RPI Broker (Mosquitto)

This broker accepts MQTT messages from multiple Raspberry Pi sensors and
provides them to the Django backend for storage and to any frontend clients
for real-time display.

## Start the broker

```bash
docker compose up -d
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
