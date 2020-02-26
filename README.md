# Elco-Remocon
Python script to retrieve information from an ELCO Heating system using the REMOCON.NET option (web based).
The script should work with other models with minor changes.

This version is made to monitoring, analytics and control for Home-Assistant using a MQTT solution.

## Dependencies (with tested version)
* $ pip install colorama==0.3.7
* $ pip install requests==2.18.4
* $ pip install beautifulsoup4==4.8.1
* $ pip install paho_mqtt==1.4.0
* A functionnal MQTT server...

## Features

* Access the REMOCON.NET web interface to retrieve information (www.remocon-net.remotethermo.com)
* Use MQTT to publish the information

## Version
* Current: Version 1.0 : Initial published version

## Preview

![Script display](https://github.com/MoBOatGVA/Rika-Firenet/blob/master/elco_display.png)

## Installation and Support

* Install python dependencies according requirements.txt
* Edit elco_config.yaml with your information
* Run using "/usr/bin/python3 elco.py" and check results
* Make sure MQTT is configured on your configuration.yaml file in Home Assitant
```
# configuration.yaml
# MQTT Broker (internal)
mqtt:
  broker: !secret mosquittoip
  username: !secret mosquittouser
  password: !secret mosquittopass
```
* Add sensors in Home-Assistant (change topic according your elco.yaml)
```
#########################################################################
#                                 RIKA                                  #
#########################################################################
sensor:
#region : Check Time
- platform: mqtt
  name: "Elco Check Time"
  force_update: True
  state_topic: "tele/elco/SENSOR"
  value_template: '{{ value_json["SENSOR"]["check_time"] }}'
#endregion

#region : Outside Temperature
- platform: mqtt
  name: "Elco Outside Temp"
  force_update: True
  state_topic: "tele/elco/SENSOR"
  value_template: '{{ value_json["SENSOR"]["outside_temp"] }}'
  unit_of_measurement: "°C"
#endregion
```
* More information can be added if needed from elco.py, line 168 (json_data=...)
  - Check json_full_from_elco.txt for all available FIRENET fields (dump from the website) NOTE: To be added soon!

## Issues & Feature Requests

* Please see the [Issues Repository](https://github.com/MoBOatGVA/Elco-Remocom/issues).

## License

This is free software under the GPL v3 open source license. Feel free to do with it what you wish, but any modification must be open sourced. A copy of the license is included.
