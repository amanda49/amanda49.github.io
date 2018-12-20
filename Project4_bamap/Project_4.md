---
title: Hawaiian Islands 
feature_image: "![project4_feature](https://user-images.githubusercontent.com/42807705/50263440-bb849a80-03e3-11e9-8fda-3168049180f0.png)"
---
<!--This is the first row of projects -->

## Relief Map

This is a relief map of the islands and surrounding water of the Hawaiian islands.
This was created by using a z factor of 900 and click on generate relief classes automatically.
By making a relief map you can see the vase difference in the elevation ranges that are
on the islands as well as in the ocean.

![relief1](https://user-images.githubusercontent.com/42807705/50250670-7fcfdd80-03af-11e9-832e-14eb1f33581e.PNG)

![relief](https://user-images.githubusercontent.com/42807705/50250671-80687400-03af-11e9-960f-7ca02daad1f7.jpg)

## Python

This code will load in a base map that can be used as a starting point to locate the area that you are looking at.
````Python
qgis.utils.iface.addRasterLayer("http://server.arcgisonline.com/arcgis/rest/services/ESRI_Imagery_World_2D/MapServer?f=json&pretty=true","raster")
````

This code will download all of the healthy coral reef sites around the Hawaiian Islands. Then the second part of the code, 
the rendering, changes the points to green, which indicates thriving reefs. The selection part of the code
allows you to pick a site name of your choosing and the site will be highlighted (in yellow) on the map. You can pick any 
site name that you wish to look at and the point will show up on the map. (As seen below on the map)

````Python
Healthy_Sites = QgsVectorLayer('F:/Final Project/Coral Reefs/Healthy_Sites.shp', 'reefs')
Healthy_Sites.isValid()
QgsProject.instance().addMapLayers([Healthy_Sites])

renderer = Healthy_Sites.renderer()
renderer
symbol = renderer.symbol()
symbol.dump()
symbol.setColor(Qt.green)
Healthy_Sites.triggerRepaint()

iface.layerTreeView().refreshLayerSymbology(Healthy_Sites.id())

selection = Healthy_Sites.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"SITE_NAME" = \'Sunset Point\''))
Healthy_Sites.selectByIds([s.id()for s in selection])

iface.mapCanvas().zoomToSelected()
````

![1](https://user-images.githubusercontent.com/42807705/50251676-a5aab180-03b2-11e9-9310-c4c63bb9870b.PNG)

This code will download all of the unhealthy coral reef sites around the Hawaiian Islands. Then the second part of the code, the rendering, changes the points to red, which indicates reefs that have diseases and or coral bleaching.
The selection part of the code allows you to pick a location of your choosing and the location will be highlighted (in yellow) on the map. You can pick any location that you wish to look at and the point will show up on the map. (As seen below on the map)

````Python
Unhealthy_Sites = QgsVectorLayer('F:/Final Project/Coral Reefs/Unhealthy_Sites.shp', 'reefs')
Unhealthy_Sites.isValid()
QgsProject.instance().addMapLayers([Unhealthy_Sites])

renderer = Unhealthy_Sites.renderer()
renderer
symbol = renderer.symbol()
symbol.dump()
symbol.setColor(Qt.red)
Unhealthy_Sites.triggerRepaint()

iface.layerTreeView().refreshLayerSymbology(Unhealthy_Sites.id())

selection = Unhealthy_Sites.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"Location" = \'Barge Harbor\''))
Unhealthy_Sites.selectByIds([s.id()for s in selection])

iface.mapCanvas().zoomToSelected()
````

![2](https://user-images.githubusercontent.com/42807705/50251674-a5aab180-03b2-11e9-80cc-8e96e99762c2.PNG)

## Islands

In this section I wanted to look at how the sea level rise would effect the Hawaiian Islands. There was 6 main islands that was
looked at. They included:

-Hawaii
-Kauai
-Lanai
-Maui
-Molokai
-Oahu

I had to bring in the shapefiles for the sea level for the different islands [NOAA](https://coast.noaa.gov/slrdata/). Then I brought in a shapefile that had the area of the islands in the attribute table. I had to use the fix
geometries tool for the islands as well as the sea level rise data and then I
clipped the sea level rise data (that were fixed) with the islands (that
were fixed). I had to do this in order to see how much of the islands were lost
to 10 feet of sea level rise. The sea level rise was in square feet and the land area
was in meters squared, so I converted everything into miles squared. I looked at
the total area of land, the total area of sea level rise (once clipped), and
the remaining land area after 10 feet squared (3.5 miles squared) of sea level
rise.

I produced all 6 islands of what they will look like now and when they have 10 feet of
sea level rise and the stats of the total area of land, total area of sea level rise, and
total area of land after sea level rise all in miles squared. (These maps are seen below) 

![hawaii1](https://user-images.githubusercontent.com/42807705/50256713-941ed500-03c5-11e9-8106-ce28997b814b.jpg)
![kauai1](https://user-images.githubusercontent.com/42807705/50256715-9719c580-03c5-11e9-94b3-46c1933046ff.jpg)
![lanai1](https://user-images.githubusercontent.com/42807705/50256716-98e38900-03c5-11e9-9057-63325ccdd01e.jpg)
![maui1](https://user-images.githubusercontent.com/42807705/50256721-a13bc400-03c5-11e9-8120-8b911b9c95bf.jpg)
![molokai1](https://user-images.githubusercontent.com/42807705/50256732-af89e000-03c5-11e9-998d-a83cf44524c6.jpg)
![oahu1](https://user-images.githubusercontent.com/42807705/50256737-bc0e3880-03c5-11e9-9923-b79a824d3e04.jpg)

## Shipwrecks

I had to bring in the shapefiles for the shipwrecks and obstructions [NOAA](https://nauticalcharts.noaa.gov/data/wrecks-and-obstructions.html), then used the extract by clip extent tool to clip them out, so the points would only show up around the islands.
I brought in a nautical map [NOAA](http://www.charts.noaa.gov/InteractiveCatalog/nrnc.shtml) and overlaid it with the raster image. I used transparency and put the transparency at 30%, that way you can see the color of the water and land a little bit better. I did this to make a heatmap of the shipwrecks and obstructions around the islands. For my heatmap I used a radius of 7,000 and had rows of 500 and columns 807 and used the blending mode burn with the color ramp reds to indicate where the majority of reefs are located at. 

This is a heatmap of the shipwrecks around the Hawaiian Islands.  

![shipwrecks](https://user-images.githubusercontent.com/42807705/50249482-2e721f00-03ac-11e9-92db-99eb28d50e1d.jpg)

This is a heatmap of the obstructions around the Hawaiian Islands. 

![obstructions](https://user-images.githubusercontent.com/42807705/50249481-2e721f00-03ac-11e9-9ba5-adf373250579.jpg)

For the AWOIS_Wrecks and ENC_Wrecks I used the following code in the field calculator
to get the years found for the shipwrecks. Then I used the merge vector layers tool
to combine the two shapefiles together to have all the shipwrecks on one file.
````Python
concat('19',substr("HISTORY",strpos("HISTORY", '/')+1,2))
````

For the obstructions I used the following code in the field calculator to get the 
years found. 
````Python
left("SORDAT",4)
````

![shipwrecks_obstructions](https://user-images.githubusercontent.com/42807705/50248793-329d3d00-03aa-11e9-87e5-524c457f2ed0.jpg)

This is a .gif that is broken up by five different time frames to illustrate when shipwrecks and obstructions were found throughout the Hawaiian Islands. The shipwrecks are in red and the obstructions are in light blue. The obstructions start in the 1924 and end in 2009, while the shipwrecks start in 1924 and end in 2017. Both the shipwrecks and obstructions end in the same year, so the next set of years can start and end in the same year. 

![ezgif com-gif-maker 1](https://user-images.githubusercontent.com/42807705/50249346-c15e8980-03ab-11e9-9ea7-2fea51437a67.gif)

## Coral reefs

Once I downloaded all the files I had to change all of my excel files into .txt files to import them. Did this by going into
layer > Delimited Text and then upload the .txt files. Then had to check off the
custom delimiters and point coordinates. The x field was Longitude and the
y field was Latitude. The projection was EPSG: 4326 - WGS 84. This had to be done in order to get all
of the coral reef points onto the map. Then I had to extract by clip extent the reefs, so they would only show up around the islands. Then I decided to change the reef locations depth into feet instead of meters.

I had to bring in the shapefiles for the reef locations, monitoring sites, marine protected areas, coral bleaching, and coral diseases [ReefBase](http://www.reefbase.org/gis_maps/datasets.aspx), then used the extract by clip extent tool to clip them out, so the points would only show up around the islands. I brought in a nautical map [NOAA](http://www.charts.noaa.gov/InteractiveCatalog/nrnc.shtml) and overlaid it with the raster image. I used transparency and put the transparency at 30%, that way you can see the color of the water and land a little bit better. I did this to make a heatmap of all of the coral reef locations, healthy coral reef locations, and unhealthy coral reef locations. For my heatmap I used a radius of 7,000 and had rows of 500 and columns 807 and used the blending mode burn with the color ramp reds to indicate where the majority of reefs are located at. 

I used the merge vector layer tool to merge the layers of all of the different healthy and the unhealthy coral reefs together. That way it can be easier to find and locate them on a map. Once I merge the vector layers together to get the unhealthy and healthy coral reefs, I then merge those two vector layers together to get all of the coral reef locations for the Hawaiian Islands.

This is a heatmap of all the coral reefs around the Hawaiian Islands.

![all_locations_heat](https://user-images.githubusercontent.com/42807705/50249484-2e721f00-03ac-11e9-8b4a-4e9e778398c5.jpg)

This is a heatmap of all the healthy coral reefs around the Hawaiian 
Islands. 

![healthy_sites](https://user-images.githubusercontent.com/42807705/50249485-2e721f00-03ac-11e9-99ea-a626dc7c7a1b.jpg)

This is a heatmap of all the unhealthy coral reefs around the Hawaiian
Islands.  

![unhealthy_sites](https://user-images.githubusercontent.com/42807705/50249483-2e721f00-03ac-11e9-828a-6e26743777b8.jpg)

![ezgif com-gif-maker 2](https://user-images.githubusercontent.com/42807705/50250300-65493480-03ae-11e9-8f16-c3f1bf865053.gif)

I made a 3D map of all the coral reef locations (that are in pink) by their
water depth's. The evaluations of the islands are also included in the 3D map
as well. For the vertical scale, it was set at 5 and for the tile resolution I made
that a 500px. Everything else on the configuration I left alone. I used my
original raster and overlaid my relief raster on top of my original to create
my 3D map. 

![top_veiw](https://user-images.githubusercontent.com/42807705/50250891-26b47980-03b0-11e9-8a1f-db09c161f29c.jpg)
![side_view](https://user-images.githubusercontent.com/42807705/50250892-274d1000-03b0-11e9-8c08-a836796581b8.jpg)
![ezgif com-gif-maker 1](https://user-images.githubusercontent.com/42807705/50250893-29af6a00-03b0-11e9-9823-066490576079.gif)
