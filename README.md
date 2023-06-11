## Installation steps for Raspberry Pi OS


### Update the system:
```
sudo apt-get update
sudo apt-get upgrade
```

###  Install docker:
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
```
##### Reboot the system

### Install docker-compose:
```
sudo pip install docker-compose
```

### Clone the git repository:
```
git clone https://github.com/kub/ha-plc.git
```

## Running / stopping HA

### Run the HA
```
docker-compose -f ha-plc/docker-compose.yaml up -d
```

### Stop the HA
```
docker-compose -f ha-plc/docker-compose.yaml down
```

## Accessing and configuring HA
- Home Assistant will be accessible on port 8123 (e.g. http://192.168.0.109:8123/).
- MQTT broker is running in the internal docker network - it is visible by other docker-compose components under hostname `mosquitto` and port `1883`
- PLCComs (Telnet service) is running on port 5010

It is necessary to provide correct mapping between PLC variables and MQTT topics. This can be done in `ha-plc/plccoms-mqtt-bridge/config.yaml` in the `var-mapping` section.
The topics are then used in the HA UI to communicate with the underlying PLC. 

## Adding MQTT broker to HA
