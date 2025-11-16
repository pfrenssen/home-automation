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
```

Restart a container

```
$ podman restart home-automation-zigbee2mqtt
```

### MQTT

Subscribe to all Zigbee2MQTT topics (from Mosquitto container)

```
$ podman exec -it home-automation-mosquitto mosquitto_sub -h localhost -p 1883 -t zigbee2mqtt/# -v
```

Subscribe from host (if mosquitto_sub is installed)

```
$ mosquitto_sub -h localhost -p 1883 -t zigbee2mqtt/# -v
```
