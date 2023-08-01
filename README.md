## Description

This tool creates CSV file from travel times/distances returned by Google Maps APIs.
You could use it for example for measuring traffic density from your home to your work.

## Installation

```
pip install python-gmaps
```

### Usage

The tool is config-driven.
Each time you run it it appends new line to CSV file with current data.

**Limitations:**
* The script does not work for routes with waypoints. Probably you should never hit this case unless you hack into the code.
* No error checking is done. If you set something incorrectly you'll see Python stacktraces.

```
$ ./travel-times -h
usage: travel-times [-h] [-v] config

Gather travel times and distances to CSV table

positional arguments:
  config         Config file with keys and locations

optional arguments:
  -h, --help     show this help message and exit
  -v, --verbose  Config file with keys and locations
```

### Config format

Config is a plain INI-file. It must start with section `[Main]` or it will not work.
Parameters `data` and `readable` are optional, all other are required.

```
[Main]

#  Your Google Maps API key
api_key = AIzaSyDYCAJi0JKw2ZuRTBrG7RaFzY821MRfET

#  From travel location
from = Moscow, Kreml'

#  To travel location
to = Moscow, Aeroport Sheremetyevo

#  CSV file to update
output = travel1.csv

#  Set to duration (default) or distance
#data = distance

#  Set to true to use human-readable format
#readable = false
```

API key should be obtained as described in https://github.com/googlemaps/google-maps-services-python#api-keys

Travel location could be specified in any string representation which Google understands.
UTF symbols (addresses in nation languages) worked for me ok but not sure they are going to work for you.

You can retrieve travel times or travel distances. This is controlled by `data` parameter.

By default values are written in metres and in seconds.
If you set `readable` to true the data will be written in human-readable format like `39 mins` or `32.1 km`
