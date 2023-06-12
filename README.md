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
⚠️ Reboot the system ⚠️

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
<img width="1237" alt="x" src="https://github.com/kub/ha-plc/assets/2393093/5ad4a0b0-8eb2-4a8a-80d2-304140d9067a">


## Adding MQTT broker to HA

<img width="1946" alt="1" src="https://github.com/kub/ha-plc/assets/2393093/47511bb8-e4ae-46fa-808c-04e7ca443e3a">
<img width="2679" alt="2" src="https://github.com/kub/ha-plc/assets/2393093/f774079c-df71-40d5-8dfd-eecd1a377375">
<img width="1722" alt="3" src="https://github.com/kub/ha-plc/assets/2393093/712ae840-3c92-4daf-9880-44d2ba10156b">
<img width="684" alt="4" src="https://github.com/kub/ha-plc/assets/2393093/2492ef9a-90b5-429f-967e-b25cb298e4dc">
<img width="709" alt="y" src="https://github.com/kub/ha-plc/assets/2393093/f1887a82-3e5e-46ea-a24f-d3a9ef707d3b">
