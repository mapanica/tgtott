# tgtott (tuani GPX to osm2gtfs timetable tool)

Extracts time data from given GPX tracks and calculates times for stops
of given OpenStreetMap route relation.

## Example Call

```
tgtott
```

## Parameters

### -b --batch

Batch mode: mobile devices stays in public transport for some time
(whole day/week) and tgtott calculates timetable from track.

### -d --debug

Prints debug information. When a path to file is given, it writes this
information to the file.

### -D --download-only

Only downloads route relations from OpenStreetMap for later to be used
offline.

### -p --path

Path to directory containing GPX tracks. Can be used multiple times to
define multiple directories containing GPX tracks.

### -r --relation

OpenStreetMap relation

#### Accepted formats

* [http[s]://]osm.org/relation/123
* [http[s]://]openstreetmap.org/relation/123
* ID (123)

### -R --refresh

Invalidates Overpass cache for used OpenStreetMap route relations.
Together with `-d` it only downloads new data and terminates afterwards.

### --refresh-all

Invalidates cache for all OpenStreetMap route relations. Together with
`-d` it only downloads new data and terminates afterwards.

### -t --track

Path to track. Can be used multiple times to define multiple tracks.

## Default Parameters

### -p --path

`.` (Current directory)

## Current Limitations

* Only works with GPX tracks of one route
* Batch mode not implemented yet

## What tgtott does exactly

* store all GPX tracks in data structure
* find common way of GPX tracks
* find OpenStreetMap route relation matching matching GPX track
* download the OpenStreetMap relation from Overpass and store its stops
and ways in a data structure
* for each GPX track
* -| find out at which time the GPX track leaves the area close to the
first stop and use this as starting time
* -| find the first GPX point close to the second stop and connect the
stop to this time
* -| do the same for all the other stops
* calculate average time differences between stops

## Design Decisions

* Fully internationalized/translatable from the start off
* First tests are written, then features are implemented
* Exceptions are used instead of sys.exit(0)
* Fully modularized so it can be used as a library
* Based on latest stable Python 3
* Performance kept in mind
* Using OpenStreetMap Public Transport Format Version 2
* Offline usage kept in mind
* Cache Overpass requests and retry them when they fail
* Easy to debug
* To be used on Linux, macOS and Windows
* Keep amount of dependencies low

## Questions to solve

* Should we rather implement our own GPX parser than using a library?
Reasons are performance and the design decision to keep amount of
dependencies low.

## tuani things

To be implemented later:

* Try to find out time differences based on day's time/weekday because
how long a trip take can depend on when it goes

## License

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You can find the full license text [here](LICENSE.markdown).
