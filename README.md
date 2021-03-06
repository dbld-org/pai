# PAI - Paradox Alarm Interface

Middleware that aims to connect to a Paradox Alarm panel, exposing the interface for monitoring and control via several technologies.
With this interface it is possible to integrate Paradox panels with HomeAssistant, OpenHAB, Homebridge or other domotics system that supports MQTT, as well as several IM methods.

It supports MG/SP/EVO panels connected through a serial port, which is present in all panels (TTL 5V), or through a USB 307 module. It also has __beta__ support to connections using the IP150 module, both directly (firmware version <4.0), and through the SITE ID (firmware versions >4.0).

Support for Magellan and Spectra panels is very stable. Support for EVO panels is being added, so YMMV. If you find a bug, please report it.


Tested in the following environment:
* Python > 3.5.2
* Mosquitto MQTT Broker >v 1.4.8
* OrangePi 2G-IOT, NanoPi NEO, and Raspberry Pi 3 through their built in Serial Port (with a level shifter!), or a USB RS232 TTL adapter (CP2102, PL2303, CH340, etc..)
* Ubuntu Server 16.04.3 LTS
* Paradox MG5050, SP7000 and EVO panels
* [Signal Cli](https://github.com/AsamK/signal-cli) through a DBUS interface
* Pushbullet.py
* SIM900 module through a serial port

For further information and detailed usage refer to the [Wiki](https://github.com/jpbarraca/pai/wiki).

## How to use

### Docker

If you have docker running, this will be the easy way:
```
docker build -t pai .
docker run -it -v <projectFolder>/config/user.py:/opt/paradox/config/user.py pai
```

### Manually

1.  Download the files in this repository and place it in some directory
```
git clone https://github.com/jpbarraca/pai.git
```

2.  Copy user.py.sample to user.py and edit it to match your setup. You only need to define the variables that you wish to override from the ```defaults.py```.
```
cd config
cp user.py.sample user.py
cd ..
```

3.  Install the python requirements.
```
pip3 install -r requirements.txt
```

If some requirement fail to install, this may not be critical.
* ```gi```, ```pygobject``` and ```pydbus``` are only required when using Signal
* ```Pushbullet.py``` and ```ws4py``` are only required when using Pushbullet
* ```paho_mqtt``` is only required for MQTT support
* ```pyserial``` is only required when connecting to the panel directly through the serial port or using a GSM modem.


4.  Run the script:
```
python3 run.py
```

If something goes wrong, you can edit the ```config/user.py``` to increase the debug level.
Check ```config/defaults.py``` for all configuration options

## Authors

* João Paulo Barraca - [@jpbarraca](https://github.com/jpbarraca) - Main code and MG/SP devices
* Ion Darie - [@iondarie](https://github.com/iondarie) - Homebridge integration
* Jevgeni Kiski - [@yozik04](https://github.com/yozik04) - EVO devices


## Acknowledgments

This work is inspired or uses parts from the following projects:

* Tertiush at https://github.com/Tertiush/ParadoxIP150v2
* Spinza at https://github.com/spinza/paradox_mqtt


## Disclaimer

Paradox, MG5050 and IP150 are registered marks of PARADOX. Other brands are owned by their respective owners.

The code was developed as a way of integrating personally owned Paradox systems, and it cannot be used for other purposes.
It is not affiliated with any company and it doesn't have have commercial intent.

The code is provided AS IS and the developers will not be held responsible for failures in the alarm systems, or any other malfunction.
