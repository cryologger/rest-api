# Cryologger REST API Documentation

## Introduction
The Cryologger API can be accessed from https://api.cryologger.org/

## API Query Format

### Parameters

**Table 1.**  List of API query parameters. 
| Parameter | Description                        | Required | Default |
|-----------|----------------------------------- |----------|---------|
| uid       | Unique instrument identifier       | Yes      |         |
| field     | Variable(s) to be queried          | No       | All     |
| records   | Number of records to be requested  | No       | 24      |

### Query Structure

As shown in Table 1, the `uid` parameter is required for all Cryologger API calls. If the `field` parameter is omitted, all the data variables shown in Tables 1 & 2 will be returned. If the `records` field is omitted, only the 24 most recent data samples will be returned.

### API Query Examples

**Base API URLs:**
```
# Automatic weather station
https://api.cryologger.org/aws

# Ice tracking beacon
https://api.cryologger.org/itb
```

**Past 24 hours of all data varaibles from a single automatic weather station**
```
https://api.cryologger.org/itb?uid=HFD
```
**500 most recent samples of wind speed from three automatic weather stations**
```
https://api.cryologger.org/aws?uid=ALW&uid=MPC&uid=NPK&field=wind_speed&records=500
```

### API Keys
An API key is required to invoke the Cryologger API, which must be provided using `x-api-key` in the header. At present, it is not possible to send an API key as query string parameter.

#### API Key Examples:

##### Curl
```
curl -H "x-api-key: 4u4en4b845anvq7isst793wg4e5y5ex2xk73nw2g" -X GET "https://api.cryologger.org/aws?uid=ALW"
```

##### Python
```
import requests
import pandas as pd
# Specify API key in header
headers = {'x-api-key': '4u4en4b845anvq7isst793wg4e5y5ex2xk73nw2g'}
# Format URL based on desired data request
url = "https://api.cryologger.org/aws?uid=ALW"
# Invoke API
response = requests.get(url, headers=headers)
# Create pandas dataframe from the API response
df = pd.read_json(response.text)
```

## Variables

Data accessible from the Cryologger API is split into two categories: 1) sensor and 2) diagnostic. Sensor variables pertain to the data that is collected from the various instruments onboard the Cryologger platform (e.g., meterology, location, etc.). Additional diagnostic variables, which are standardized across all Cryologer applications, are also available upon request. These variables provide detailed information regarding the operational health of the equipment.

It is important to note the availability of 

### Automatic Weather Station (AWS)

**Table 2.**  List of meterological varaibles available to be queried from the Cryologger AWS API. 
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
| latitude                 | degree | Latitude                                                            |
| longitude                | degree | Longitude                                                           |
| satellites               |        | Number of satellites in view                                        |
| hdop                     |        | Horizontal dilution of precision (HDOP)                             |
| voltage                  | V      | Battery voltage                                                     |


## Cryologger Deployments

| Instrument                | Unique ID | Latitude   | Longitude  | Location             | Place Name
|---------------------------|:---------:|------------|------------|----------------------|------------------|
| Automatic Weather Station	| ALW	      |            |            | Arctic Bay, Nunavut  | Qakuqtaqtujut    |
| Automatic Weather Station | MPC	      |            |            | Arctic Bay, Nunavut  | Pullataujaq      |
| Automatic Weather Station	| NPK	      |            |            | Milne Fiord, Nunavut |                  |
| Automatic Weather Station | YYP	      |            |            | Milne Fiord, Nunavut |                  |
