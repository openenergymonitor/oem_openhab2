# OpenHAB2

OpenEnergyMonitor config for OpenHAB2: specifically for running on emonPi with MQTT.

**IN DEVELOPMENT**

***

## Install OpenHAB 

Taken from: http://docs.openhab.org/installation/linux.html

```
echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/webupd8team-java.list
echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | sudo tee -a /etc/apt/sources.list.d/webupd8team-java.list
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
sudo apt-get update
sudo apt-get install oracle-java8-installer
sudo apt-get install oracle-java8-set-default

wget -qO - 'https://bintray.com/user/downloadSubjectPublicKey?username=openhab' | sudo apt-key add -
echo 'deb http://dl.bintray.com/openhab/apt-repo2 stable main' | sudo tee /etc/apt/sources.list.d/openhab2.list

sudo apt-get update
sudo apt-get install

sudo systemctl start openhab2.service
sudo systemctl status openhab2.service
sudo systemctl daemon-reload
sudo systemctl enable openhab2.service
```

Openhabe should now be running, browse to http://emonpi:8080

## Addons 

Install addons via web interface UI

### MQTT

Install MQTT binding via the interface then edit

`/etc/openhab2/services/mqtt.cfg`

Add:


```
mosquitto.url=tcp://localhost:1883
mosquitto.user=emonpi
mosquitto.pwd=emonpimqtt2016
mosquitto.qos=2
```

`mosquitto` is the name given to the mqtt broker


