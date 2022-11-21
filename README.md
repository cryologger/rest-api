# Cryologger REST API Documentation

## Introduction
The Cryologger API can be accessed from https://api.cryologger.org/

## API Query Format

### Parameters

| Parameter | Description                        | Required |
|-----------|----------------------------------- |----------|
| imei      | Unique identifier                  | Yes      |
| field     | Variable(s) to be queried          | No       |
| records   | Number of records to be requested  | No       |

### Query Structure


#### Automatic Weather Station (AWS)

Base API URL:
* ```https://api.cryologger.org/aws```

Example API query:
* ```https://api.cryologger.org/aws?imei=300434063398110&field=air_temperature&records=5```


#### Ice Tracking Beacon (AWS)

Base API URL:
* ```https://api.cryologger.org/itb```

Example API query:
```https://api.cryologger.org/itb?imei=300434063298940&field=latitude&field=longitude&records=5```


## Variables

Data that can be accessed from the Cryologger API is split into two categories: 1) sensor and 2) diagnostic. The sensor variables pertain to the data that is collected from the various instruments onboard the Cryologger platform (e.g., meterological). The diagnostic variables are standardized across all Cryologer applications provide detailed information regarding the operational health of the equipment. 

### Automatic Weather Station (AWS)

#### Meterological Data Variables
**Table 1.**  List of CF convention compliant meterological varaibles that can be queried from the Cryologger API. 
| Variable Name            | Unit   | Description                                                         | CF compliant |
|--------------------------|--------|---------------------------------------------------------------------|:------------:|
| time                     | s      | Number of seconds since January 1, 1970 00:00:00 UTC (Unix time)    |      Yes     |
| air_temperature          | K      | Air temperature                                                     |      Yes     |
| relative_humidity        | %      | Relative humidity                                                   |      Yes     |
| air_pressure             | Pa     | Air pressure                                                        |      Yes     |
| solar_irradiance         | W m-2  | Solar irradiance                                                    |      Yes     |
| wind_speed               | m s-1  | Wind speed                                                          |      Yes     |
| wind_from_direction      | degree | Wind direction                                                      |      Yes     |
| wind_speed_of_gust       | m s-1  | Wind gust speed                                                     |      Yes     |
| wind_gust_from_direction | degree | Wind gust direction                                                 |      Yes     |
| platform_pitch           | degree | Pitch angle                                                         |      Yes     |
| platform_roll            | degree | Roll angle                                                          |      Yes     |

### Ice Tracking Beacon (ITB)

#### Sensor Data Variables
**Table 3.**  List of sensor datas that can be queried from the Cryologger ITB API. 
| Variable Name            | Unit   | Description                                                         | CF compliant |
|--------------------------|--------|---------------------------------------------------------------------|:------------:|
| time                     | s      | Number of seconds since January 1, 1970 00:00:00 UTC (Unix time)    |      Yes     |
| air_temperature          | K      | Air temperature                                                     |      Yes     |
| relative_humidity        | %      | Relative humidity                                                   |      Yes     |
| air_pressure             | Pa     | Air pressure                                                        |      Yes     |
| solar_irradiance         | W m-2  | Solar irradiance                                                    |      Yes     |
| wind_speed               | m s-1  | Wind speed                                                          |      Yes     |
| wind_from_direction      | degree | Wind direction                                                      |      Yes     |
| wind_speed_of_gust       | m s-1  | Wind gust speed                                                     |      Yes     |
| wind_gust_from_direction | degree | Wind gust direction                                                 |      Yes     |
| platform_pitch           | degree | Pitch angle                                                         |      Yes     |
| platform_roll            | degree | Roll angle                                                          |      Yes     |

### Standard Diagnostic Variables
**Table 2.**  List of diagnostic varaibles that can be queried from the Cryologger API.
| Variable Name              |     Unit     | Description                                            |
|----------------------------|:------------:|--------------------------------------------------------|
| imei                       |              | International Mobile Equipment Identity                |
| momsn                      |              | Mobile Originated Message Sequence Number              |
| transmit_time              |    ISO8601   | Iridium Short Burst Data (SBD) transmission time (UTC) |
| iridium_latitude           | degree_north | Estimated latitude                                     |
| iridium_longitude          |  degree_west | Estimated longitude                                    |
| iridium_cep                |      km      | Estimated radius around IMEI location                  |
| data                       |  hexadecimal | Iridium SBD data payload                               |
| internal_air_temperature   |       °C     | Internal air temperature                               |
| internal_relative_humidity |       %      | Internal humidity                                      |
| internal_air_pressure      |      Pa      | Internal air pressure                                  |
| voltage                    |       V      | Battery voltage                                        |
| transmit_duration          |       s      | Duration of the previous Iridium SBD transmission      |
| transmit_status            |              | Iridium transmission diagnostic code                   |
| message_counter            |              | Counter to track program iterations/resets             |
