# GIS Lab project 2019

Project repository for the 2019-2020 POLIMI Geographic Information Systems course.

Group members:
- Mikael Vaaltola
- Yasin Ozturk
- Revnak Sayin
- Firmino Mucucete

## Data processing steps
- Join all measuring points into a single .csv
- Import points into QGIS and save to a spatial format
- Remove out bad lightning measurements from 2019-12-08
- Create 15m buffer for road
- Spatial join road fid from buffer to points
- Manually assign matching road fid to seven unassigned points. All points were within few metres of nearest road so it was easy to guess best match
- Remove duplicate points (fid not unique) created by join (most time consuming process so far). First create new field isduplicate, populate by field calc using a CASE, described [here](https://gis.stackexchange.com/a/249976), hen manually go through each case.
- Separate filtered points to layers by measurement type
- Aggregate values for measurements with same road fid - average or sum
- Join aggregated values from created layers to road network by road fid
- Manually fill missing values based on neighboring segments and omitted measurements
- PLOS was then calculated with the expression:

```6.0468 + 0.0091 * ("vm" / (4 * "nth")) + 4 * (("sr" * 0.621371) / 100)^2 - 1.2276 * ln(("wv" * 3.28084) + 0.5 * ("w1" * 3.28084) + 50 * "ppk" + ("wbuff" * 3.28084) * 5.37 + ("waa" * 3.28084) * "fsw")```