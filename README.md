# Ground Track Generator

A utility to write satellite ground tracks as GIS-compatible shapefiles. Orbits are modelled with Dan Warner's [C++ SGP4 library](http://www.danrw.com/sgp4-satellite.php), based on ["Revisiting Spacetrack Report #3"](http://www.celestrak.com/publications/AIAA/2006-6753/). Two-line element (TLE) sets of orbit characteristics are required as input; TLEs for a great many satellites [are available from CelesTrak](http://celestrak.com/NORAD/elements/). Data is output using [Shapelib](http://shapelib.maptools.org/).

## Example

Here is an example plot (created with [Indiemapper](http://indiemapper.com/)) of the International Space Station's ground track:

![ISS ground track](https://github.com/anoved/Ground-Track-Generator/raw/master/test/iss2.png)

The following two-line element set (`iss.tle`) was used:

	ISS (ZARYA)             
	1 25544U 98067A   12079.89583855  .00016581  00000-0  21080-3 0  2156
	2 25544  51.6414 209.7068 0016865 175.1468 330.0443 15.59367837764090

The points were generated with the following command:

	gtg --input iss.tle --start 1332254084 --output iss

The lines were generated by re-running the command with `--format line`. The `--start` option specifies when to start the ground trace. Valid arguments are `now`, `epoch` (the reference date of the TLE), a timestamp in the exact format of `YYYY-MM-DD HH:MM:SS.SSSSSS UTC`, or a number representing the UNIX time (seconds since 00:00:00 January 1 1970; `1332254084` is sometime on March 20, 2012). By default, `gtg` outputs 100 points at 1-minute intervals. (The output interval and duration is configurable.)

## To-do

- **Write test suite**
- Handle multiple TLEs (output multiple shapefiles, named for TLE identifier, or output a single shapefile, distinguished by attribute field)
