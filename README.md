# ginlong-scraper-hass

A HACS integration that scrapes PV statistics from the Ginlong (Solis) monitor pages and outputs it to MQTT (default), InfluxDB or PVOutput. Using MQTT you can then create sensors in Home Assistant to track your energy usage. I have used this for a Solis inverter but there is a possibility it also works with the following inverters: Omnik Solar, Solarman and Trannergy Inverters.

This is a fork of the excellent ginlong-scraper by dkruyt: https://hub.docker.com/repository/docker/dkruyt/ginlong-scraper

In the case of two inverters (see note below) once you have the deviceid you can set up two seperate docker containers
and just vary the deviceId in the environment variables.

## Configuration

### Environment variables

| Environment variable      | Required | Description                                                                                          | Default value   |
|---------------------------|----------|------------------------------------------------------------------------------------------------------|-----------------|
| LOG_LEVEL                 | No       | Logging level (ERROR, INFO, DEBUG)                                                                   | `INFO`          |
| GINLONG_USERNAME          | Yes      | Ginlong Solis username                                                                               | *empty*         |
| GINLONG_PASSWORD          | Yes      | Ginlong Solis password                                                                               | *empty*         |
| GINLONG_DOMAIN            | No       | Ginlong Solis domain                                                                                 | `m.ginlong.com` |
| GINLONG_LANG              | No       | Ginlong Solis language                                                                               | `2` *(English)* |
| GINLONG_DEVICE_ID         | No       | Ginlong Solis device ID<br/>(only required if auto-detect fails or if you have more than one device) | *empty*         |
| USE_MQTT                  | No       | Set to true if you want to use MQTT as output                                                        | `true`          |
| MQTT_CLIENT_ID            | No       | MQTT client ID                                                                                       | `pv`            |
| MQTT_SERVER               | No       | MQTT server                                                                                          | `localhost`     |
| MQTT_USERNAME             | No       | MQTT username                                                                                        | *empty*         |
| MQTT_PASSWORD             | No       | MQTT password                                                                                        | *empty*         |
| USE_INFLUX                | No       | Set to true if you want to use InfluxDB as output                                                    | `false`         |
| INFLUX_DATABASE           | No       | InfluxDB DB name                                                                                     | `influxdb`      |
| INFLUX_SERVER             | No       | InfluxDB server                                                                                      | `localhost`     |
| INFLUX_PORT               | No       | InfluxDB server port                                                                                 | `8086`          |
| INFLUX_USER               | No       | InfluxDB User                                                                                        | *empty*         |
| INFLUX_PASSWORD           | No       | InfluxDB Password                                                                                    | *empty*         |
| INFLUX_MEASUREMENT        | No       | InfluxDB measurement type                                                                            | `PV`            |
| USE_PVOUTPUT              | No       | Set to true if you want to use PvOutput as output                                                    | `false`         |
| PVOUTPUT_API_KEY          | No       | PvOutput API key                                                                                     | *empty*         |
| PVOUTPUT_SYSTEM_ID        | No       | PvOutput system ID                                                                                   | *empty*         |
| TZ                        | No       | TimeZone e.g Australia/Sydney                                                                        | *empty*         |

Note that if you have more than 1 device - then it is not readily apparent where to get the Device ID
In that case - setup the script, and set LOG_LEVEL to DEBUG, then view the logs and search for deviceId - 
this will list the IDs of each inverter.
