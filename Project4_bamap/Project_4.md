---
title: Hawaiian Islands 
---
<!--This is the first row of projects -->

## Relief Map

I made a relief map of the islands and surrounding water of the Hawaiian islands.
I made the z factor 900 and clicked on generate relief classes automatically.
I decided on making a relief map to show how different the elevation ranges are
on the islands as well as in the ocean.

![relief1](https://user-images.githubusercontent.com/42807705/50250670-7fcfdd80-03af-11e9-832e-14eb1f33581e.PNG)

![relief](https://user-images.githubusercontent.com/42807705/50250671-80687400-03af-11e9-960f-7ca02daad1f7.jpg)

## Python

Loaded in a base map using this code.
````Python
qgis.utils.iface.addRasterLayer("http://server.arcgisonline.com/arcgis/rest/services/ESRI_Imagery_World_2D/MapServer?f=json&pretty=true","raster")
````

This code will download all of the healthy coral reef sites that way you can see
them all in the Hawaiian Islands. Then the second part of the code, the rendering, changes the
points to green, which indicates thriving reefs. The selection part of the code
allows you to pick a site name of your choosing and the site will be highlighted
on the map.

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

This code will download all of the unhealthy coral reef sites that way you can see
them all in the Hawaiian Islands. Then the second part of the code, the rendering, changes the
points to red, which indicates reefs that have diseases and or coral bleaching.
The selection part of the code allows you to pick a site name of your choosing
and the site will be highlighted on the map.

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

## Islands

Brought in the shapefiles for the water for the different islands that had
the sea level as is and the sea level at 10 feet. Then I brought in a shapefile
that had the area of the islands in the attribute table. I had to use the fix
geometries tool for the islands as well as the sea level rise data and then I
had to clip the sea level rise data (that were fixed) with the islands (that
were fixed). I had to do this in order to see how much of the islands were lost
to 10 feet of water. The sea level rise was in square feet and the land area
was in meters squared, so I converted everything into miles squared. I looked at
the total area of land, the total area of sea level rise (once clipped), and
the remaining land area after 10 feet squared (3.5 miles squared) of sea level
rise.

I produced all 6 islands of what they will look like when they have 10 feet of
water and the stats of the total area of land, total area of sea level rise, and
total area of land after sea level rise all in miles squared.

## shipwrecks

Brought in the shapefiles for the shipwrecks and obstructions, then used the extract by 
clip extent to clip them out, so the points would only show up around the islands.
I brought in a nautical map and overlaid it with the raster image. I used transparency
and put the transparency to 30%, that way you can see the color of the water and 
land a little bit better. I did this to make a heatmap of all of the coral 
reef locations, healthy coral reef locations, and unhealthy coral reef locations.
For my heatmap I used a radius of 7,000 and had rows of 500 and columns 807 and
I used the blending mode burn to with the color ramp reds to indicate where the
majority of reefs are located at.

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

![ezgif com-gif-maker 1](https://user-images.githubusercontent.com/42807705/50249346-c15e8980-03ab-11e9-9ea7-2fea51437a67.gif)

## Coral reefs

Had to change all of my excel files into .txt files to import them. Had go into
layer > Delimited Text and then upload the .txt files. Had to check off the
custom delimiters and point coordinates. the x field was Longitude and the
y field was Latitude. The projection was EPSG: 4326 - WGS 84. This was to get all
of my coral reef points onto the map. Then I had to extract by clip extent the
reefs, so they would only show up around the islands. I changed the reef locations
depth into feet instead of meters.

I brought in a nautical map and overlaid it with the raster image. I used transparency
and put the transparency to 30%, that way you can see the color of the water and 
land a little bit better. I did this to make a heatmap of all of the coral 
reef locations, healthy coral reef locations, and unhealthy coral reef locations.
For my heatmap I used a radius of 7,000 and had rows of 500 and columns 807 and
I used the blending mode burn to with the color ramp reds to indicate where the
majority of reefs are located at.

I used the merge vector layer tool to merge the layers of the healthy and the
unhealthy coral reefs together. That way it can be easier to find and locate
them. Once I merge the vector layers together to get the unhealthy and healthy
coral reefs, I then merge those two vector layers together to get all of the
coral reef locations for the Hawaiian Islands.

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
as well. For the vertical scale it was a 5 and for the tile resolution I made
that a 500px. Everything else on the configuration I left alone. I used my
original raster and overlaid my relief raster on top of my original to create
my 3D map.
