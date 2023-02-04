# Cryologger REST API Documentation

## Introduction
The Cryologger API can be accessed from https://api.cryologger.org/

## API Query Format

### Parameters

| Parameter | Description                        | Required |
|-----------|----------------------------------- |----------|
| uid       | Unique identifier                  | Yes      |
| field     | Variable(s) to be queried          | No       |
| records   | Number of records to be requested  | No       |

### Query Structure


#### Automatic Weather Station (AWS)

Base API URL:
* ```https://api.cryologger.org/aws```

Example API query:
* ```https://api.cryologger.org/aws?uid=ALW&field=air_temperature&records=24```


#### Ice Tracking Beacon (AWS)

Base API URL:
* ```https://api.cryologger.org/itb```

Example API query:
```https://api.cryologger.org/itb?uid=HFD&field=latitude&field=longitude&records=24```


## Variables

Data that can be accessed from the Cryologger API is split into two categories: 1) sensor and 2) diagnostic. The sensor variables pertain to the data that is collected from the various instruments onboard the Cryologger platform (e.g., meterological). The diagnostic variables are standardized across all Cryologer applications provide detailed information regarding the operational health of the equipment. 

### Automatic Weather Station (AWS)

#### Meterological Data Variables
**Table 1.**  List of meterological varaibles that can be queried from the Cryologger AWS API. 
| Variable Name            | Unit   | Description                                                         | 
|--------------------------|--------|---------------------------------------------------------------------|
| unixtime                 | s      | Number of seconds since January 1, 1970 00:00:00 UTC (Unix time)    |
| temperature_int          | C      | Internal air temperature                                            |
| humidity_int             | %      | Internal relative humidity                                          |
| pressure_int             | Pa     | Internal air pressure                                               |
| temperature_ext          | C      | Air temperature                                                     |
| humidity_ext             | %      | Relative humidity                                                   |
| pressure_ext             | Pa     | Air pressure                                                        |
| solar                    | W m-2  | Solar irradiance                                                    |
| wind_speed               | km h-1 | Wind speed                                                          |
| wind_direction           | degree | Wind direction                                                      |
| wind_gust_speed          | km h-1 | Wind gust speed                                                     |
| wind_gust_direction      | degree | Wind gust direction                                                 |
| pitch                    | degree | Pitch angle                                                         |
| roll                     | degree | Roll angle                                                          |
| voltage                  | V      | Battery voltage                                                     |

### Ice Tracking Beacon (ITB)

#### Sensor Data Variables
**Table 3.**  List of sensor data that can be queried from the Cryologger ITB API. 
| Variable Name            | Unit   | Description                                                         | 
|--------------------------|--------|---------------------------------------------------------------------|
| unixtime                 | s      | Number of seconds since January 1, 1970 00:00:00 UTC (Unix time)    |
| temperature_int          | C      | Internal air temperature                                            |
| humidity_int             | %      | Internal relative humidity                                          |
| pressure_int             | Pa     | Internal air pressure                                               |
| pitch                    | degree | Pitch angle                                                         |
| roll                     | degree | Roll angle                                                          |
| heading                  | degree | Tilt-compensated heading                                            |
| latitude                 | degree | Tilt-compensated heading                                            |
| longitude                | degree | Tilt-compensated heading                                            |
| satellites               |        | Number of satellites in view                                        |
| hdop                     |        | HDOP                                                                |
| voltage                  | V      | Battery voltage                                                     |
