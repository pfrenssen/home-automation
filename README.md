Home automation
===============

## Requirements

* Podman
* Set up lingering for your user.

```
# loginctl enable-linger ha
```

## Quick commands

Start the stack.

```
$ podman kube play kube/home-automation.yaml
```

Stop the stack.

```
$ podman kube down kube/home-automation.yaml
```

Show pod logs

```
$ podman pod logs home-automation
```

Follow logs live

```
$ podman pod logs -f home-automation
```

Container logs

```
$ podman logs home-automation-zigbee2mqtt
$ podman logs home-automation-mosquitto
$ podman logs home-automation-homeassistant
```

Restart a container

```
$ podman restart home-automation-zigbee2mqtt
$ podman restart home-automation-homeassistant
```

## Services

- **Mosquitto MQTT Broker**: Port 1883
- **Zigbee2MQTT**: Port 8080 (Frontend)
- **Home Assistant**: Port 8123 (Web UI)

## Initial Setup

After starting the stack for the first time:

1. Access Home Assistant at http://localhost:8123
2. Create your admin user account
3. Complete the onboarding process
4. MQTT and Zigbee2MQTT devices should be auto-discovered via MQTT integration

### MQTT

Subscribe to all Zigbee2MQTT topics (from Mosquitto container)

```
$ podman exec -it home-automation-mosquitto mosquitto_sub -h localhost -p 1883 -t zigbee2mqtt/# -v
```

Subscribe from host (if mosquitto_sub is installed)

```
$ mosquitto_sub -h localhost -p 1883 -t zigbee2mqtt/# -v
```
