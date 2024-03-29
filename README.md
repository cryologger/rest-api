# Cryologger REST API Documentation

## Introduction
The Cryologger REST API is a new way to access data collected from deployed Cryologger instruments. Data can be easily accessed in a standard JSON format. 

## API Description

```
# Automatic weather station
https://api.cryologger.org/aws

# Ice tracking beacon
https://api.cryologger.org/itb
```

### Parameters

**Table 1.**  List of available API query parameters and associated properties. 
| Parameter | Description                        | Required | Default |
|-----------|----------------------------------- |----------|---------|
| uid       | Unique instrument identifier       | Yes      |         |
| field     | Variable(s) to be queried          | No       | All     |
| records   | Number of records to be requested  | No       | 24      |

### Query Structure

The API query parameters are shown in Table 1. The `uid` parameter is required for all Cryologger API calls. The `field` parameter is optional, however if omitted, all data variables listed in Tables 1 & 2 will be returned. The `records` field is also optional, and if omitted, only the 24 most recent data samples will be returned.

### API Query Examples

Request past 24 hours of all data varaibles from a single automatic weather station
```
https://api.cryologger.org/itb?uid=HFD
```
Request 500 most recent samples of wind speed from three different weather stations
```
https://api.cryologger.org/aws?uid=ALW&uid=MPC&uid=NPK&field=wind_speed&records=500
```

### API Keys
An API key is required to invoke the Cryologger API, which must be provided using `x-api-key` in the header. At present, it is not possible to send an API key as query string parameter.

#### API Key Examples:

##### Curl
```
curl -H "x-api-key: 4u4en4b845anvq7isst793wg4e5y5ex2xk73nw2g" -X GET "https://api.cryologger.org/aws?uid=NPK&field=temperature_ext&field=wind_speed&records=10"
```

##### Python
```
import requests
import pandas as pd
# Specify API key in header
headers = {'x-api-key': '4u4en4b845anvq7isst793wg4e5y5ex2xk73nw2g'}
# Format URL based on desired data request
url = "https://api.cryologger.org/aws?uid=NPK&field=temperature_ext&field=wind_speed&records=10"
# Invoke API
response = requests.get(url, headers=headers)
# Create pandas dataframe from the API response
df = pd.read_json(response.text)
```

#### API JSON Response:

```
[{"uid": "NPK", "unixtime": 1675947601, "temperature_ext": -30.86, "wind_speed": 0.16}, {"uid": "NPK", "unixtime": 1675944001, "temperature_ext": -31.45, "wind_speed": 0.0}, {"uid": "NPK", "unixtime": 1675940401, "temperature_ext": -31.45, "wind_speed": 0.33}, {"uid": "NPK", "unixtime": 1675936801, "temperature_ext": -30.98, "wind_speed": 0.16}, {"uid": "NPK", "unixtime": 1675933201, "temperature_ext": -29.54, "wind_speed": 0.22}, {"uid": "NPK", "unixtime": 1675929601, "temperature_ext": -28.76, "wind_speed": 0.16}, {"uid": "NPK", "unixtime": 1675926001, "temperature_ext": -28.67, "wind_speed": 0.02}, {"uid": "NPK", "unixtime": 1675922401, "temperature_ext": -29.28, "wind_speed": 0.36}, {"uid": "NPK", "unixtime": 1675918801, "temperature_ext": -30.08, "wind_speed": 0.27}, {"uid": "NPK", "unixtime": 1675915201, "temperature_ext": -30.84, "wind_speed": 0.3}]
```

## Variables

Data accessible from the Cryologger API is split into two categories: 1) sensor and 2) diagnostic. Sensor variables pertain to the data that is collected from the various instruments onboard the Cryologger platform (e.g., meterology, location, etc.). Additional diagnostic variables, which are standardized across all Cryologer applications, are also available upon request. These variables provide detailed information regarding the operational health of the equipment. It is important to note the availability of weather variables may vary between stations.

### Automatic Weather Station (AWS)

**Table 2.**  List of meterological varaibles available to be queried from the Cryologger AWS API. 
| Variable Name            | Unit   | Description                                                         | CF Convention Equivalent |
|--------------------------|--------|---------------------------------------------------------------------|--------------------------|
| unixtime                 | s      | Number of seconds since January 1, 1970 00:00:00 UTC (Unix time)    | time                     |
| temperature_int          | C      | Internal air temperature                                            |                          |
| humidity_int             | %      | Internal relative humidity                                          |                          |
| pressure_int             | hPa    | Internal air pressure                                               |                          |
| temperature_ext          | C      | Air temperature                                                     | air_temperature          |
| humidity_ext             | %      | Relative humidity                                                   | relative_humidity        |
| pressure_ext             | hPa    | Air pressure                                                        | air_pressure             |
| solar                    | W m-2  | Solar irradiance                                                    | solar_irradiance         |
| snow_depth               | cm     | Snow depth                                                          |                          |
| wind_speed               | m s-1  | Wind speed                                                          | wind_speed               |
| wind_direction           | degree | Wind direction                                                      | wind_from_direction      |
| wind_gust_speed          | m s-1  | Wind gust speed                                                     | wind_speed_of_gust       |
| wind_gust_direction      | degree | Wind gust direction                                                 | wind_gust_from_direction |
| pitch                    | degree | Pitch angle of weather station                                      | platform_pitch           |
| roll                     | degree | Roll angle of weather station                                       | platform_roll            |
| voltage                  | V      | Battery voltage                                                     |                          |

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

### Data Quality

Please note: The data are intended solely for informational purposes and the availability or delivery of data is not guaranteed. The data has not undergone quality control checks and may be subject to change.

## Cryologger Deployments

### Automatic Weather Station
**Table 4.**  List of deployed weather stations and locations that can be queried from the Cryologger ITB API. 
| Unique ID | Latitude   | Longitude  | Location             | Name                      | Place Name       |
|:---------:|------------|------------|----------------------|---------------------------|------------------|
| ALW	      | 73.56087   | -83.76105  | Arctic Bay, Nunavut  | Aqiggilik                 | ᐊᕿᒋᓕᒃ           |
| MPC	      | 73.52923   | -85.44611  | Arctic Bay, Nunavut  | Innaarulaalikuluup Nuvua  | ᐃᓐᓈᕈᓛᓕᑯᓘᑉ ᓄᕗᐊ |
| VUU	      | 72.73615   | -85.91475  | Arctic Bay, Nunavut  | Qikiqtatannak             | ᕿᑭᖅᑕᑕᓐᓇᒃ        |
| TDY       | 70.12236   | -82.21672  | Igloolik, Nunavut    | Ivisaaruqtuuq             | ᐃᕕᓵᕈᖅᑑᖅ         |
| LVY       | 69.85861   | -85.54392  | Igloolik, Nunavut    | Kalliraaq                 | ᑲᓪᓕᕌᖅ            |
| UBY       | 69.57053   | -80.29736  | Igloolik, Nunavut    | Kapuiviit Nuvua           | ᑲᐳᐃᕖᑦ ᓄᕗᐊ       |
| YBL       | 69.82586   | -82.13961  | Igloolik, Nunavut    | Naujaaruluit              | ᓇᐅᔮᕈᓗᐃᑦ          |
| ZTJ       | 69.82437   | -77.67336  | Igloolik, Nunavut    | Nuvuit                    | ᓄᕗᐃᑦ             |
| OEG       | 69.39090   | -81.79963  | Igloolik, Nunavut    | Qalirusiq                 | ᖃᓕᕈᓯᖅ            |
| VKP	      | 72.84904   | -76.11705  | Pond Inlet, Nunavut  | Sannirut                  | ᓴᓐᓂᕈᑦ             |
| LOA	      | 72.48496   | -79.75987  | Pond Inlet, Nunavut  | Taqqajaat                 | ᑐᖅᑲᔮᑦ             |
| NPK	      | 82.46248   | -80.73657  | Milne Fiord, Nunavut | Purple Valley             |                   |
| FON	      | 82.71045   | -81.28070  | Milne Fiord, Nunavut | Milne Ice Shelf           |                   |


**Table 5.**  List of weather stations to be deployed.
| Unique ID | Latitude   | Longitude  | Location             | Name                  | Place Name    |
|:---------:|------------|------------|----------------------|-----------------------|---------------|
||||||

