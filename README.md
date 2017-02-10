# OpenHAB2

OpenEnergyMonitor config for OpenHAB2: specifically for running on emonPi with MQTT.

**IN DEVELOPMENT**

***

## Install OpenHAB

Standard install instructions taken from: http://docs.openhab.org/installation/linux.html

**Install Java 8*

*Java 8 is already installed on latest RasPi image, if it's not then:*

```
echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/webupd8team-java.list
echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | sudo tee -a /etc/apt/sources.list.d/webupd8team-java.list
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
sudo apt-get update
sudo apt-get install oracle-java8-installer
sudo apt-get install oracle-java8-set-default
```

**Intall OpenHAB**

```
wget -qO - 'https://bintray.com/user/downloadSubjectPublicKey?username=openhab' | sudo apt-key add -
echo 'deb http://dl.bintray.com/openhab/apt-repo2 stable main' | sudo tee /etc/apt/sources.list.d/openhab2.list

sudo apt-get update
sudo apt-get install openhab2

sudo systemctl enable openhab2
sudo systemctl daemon-reload
sudo systemctl start openhab2
sudo systemctl status openhab2
```

Openhab should now be running, browse to http://emonpi:8080

## emonSD (emonPi) Specific Instructions

emonSD runs teh root FS in read only (ro) mode. `var/log` is mounted in RAM as `tmpfs` and is not peristant between boots.

### Create Logfile

Add to `etc/rc.local`

```
mkdir /var/log/openhab2
chown -R openhab:openhab /var/log/openhab2
```



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
