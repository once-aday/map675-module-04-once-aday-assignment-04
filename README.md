# map675-module-04-once-aday-assignment-04

Dataset to map (Create Tileset from)

Mumbai (India) - Land Use/Land Cover Map (ESA EO4SD-Urban)

https://datacatalog.worldbank.org/dataset/mumbai-india-land-useland-cover-map-esa-eo4sd-urban

Reproject and convert to json
`mapshaper eo4sd_mumbai_lulcvhr_2005/EO4SD_MUMBAI_LULCVHR_2005.shp -proj wgs84 -
o land_use_mumbai.json`

I am going to switch datasets to one that spans a larger area..

Indian Village Boundaries (Maps)

http://projects.datameet.org/indian_village_boundaries/kl/

State: Kerala

Total Villages and Towns: 1533
Census State code: 32
Short Name: KL


There were zoom limits put into place because of the complexity of the dataset.

>Zoom extent
>z8 – z14. Data will not be visible below z8. Data will be overzoomed to z22, but simplified past 14. Learn how to >adjust zoom extent

https://docs.mapbox.com/help/troubleshooting/adjust-tileset-zoom-extent/


I needed to modify the paint properties to make the dataset appear:
https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-fill-outline-color

If you don't zoom into the allowed zoom levels you won't see the layer, this can be deceptive if you think there is any other reason the layer isn't showing up (can be hard to debug because no error occurs).

I think sometimes there also may be a lag from when you update a tileset on mapbox and when it is available to appear on a web map because I was getting 404 errors for a while and they seemed to go away on their own.

<h2> Creating Raster Tileset from David Rumsey Collection</h2>

I am using this old map of Wales and England

https://davidrumsey.georeferencer.com/maps/261f4dbc-2aff-5669-aed0-c0310620e268/

I created an account with Georeferencer.com and downloaded the Geotiff of the map from the DR website.

ad43eec5-94e2-5236-8b15-ff53cb5b606d-2020-01-30T14_06_04.417465Z.tif

Gdal commands for converting Tif (gdal for rasters, ogr for vectors)

```
Devins-MacBook-Pro:pre_data devin$ gdalinfo ad43eec5-94e2-5236-8b15-ff53cb5b606d-2020-01-30T14_06_04.417465Z.tif
Driver: GTiff/GeoTIFF
Files: ad43eec5-94e2-5236-8b15-ff53cb5b606d-2020-01-30T14_06_04.417465Z.tif
Size is 5760, 5006
Coordinate System is:
PROJCRS["WGS 84 / Pseudo-Mercator",
```

Simplify raster using gdaltranslate
```
gdal_translate -co COMPRESS=JPEG -co TILED=YES ad43eec5-94e2-5236-8b15-ff53cb5b606d-2
020-01-30T14_06_04.417465Z.tif bristol_channel.tif
Input file size is 5760, 5006
0...10...20...30...40...50...60...70...80...90...100 - done.
```

File Size dramatically reduced:
note: -h flag shows file size in human readable format (MBs)

```
Devins-MacBook-Pro:pre_data devin$ ls -lh
total 104816
-rw-r--r--@ 1 devin  staff    45M Sep  8 12:19 ad43eec5-94e2-5236-8b15-ff53cb5b606d-2020-01-30T14_06_04.417465Z.tif
-rw-r--r--  1 devin  staff   6.2M Sep  8 12:25 bristol_channel.tif
```
http://blog.cleverelephant.ca/2015/02/geotiff-compression-for-dummies.html
