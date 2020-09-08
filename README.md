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


I needed to modify the pain properties to make the dataset appear:
https://docs.mapbox.com/mapbox-gl-js/style-spec/layers/#paint-fill-fill-outline-color

If you don't zoom into the allowed zoom levels you won't see the layer, this can be deceptive if you think there is any other reason the layer isn't showing up (can be hard to debug because no error occurs).

I think sometimes there also may be a lag from when you update a tileset on mapbox and when it is available to appear on a web map because I was getting 404 errors for a while and they seemed to go away on their own.
