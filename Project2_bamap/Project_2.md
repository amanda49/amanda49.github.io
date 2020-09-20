---
title: Shipwrecks 
feature_image: "![project2_feature](https://user-images.githubusercontent.com/42807705/50263376-6ea0c400-03e3-11e9-8312-aba5f22afef2.png)"
---
<!--This is the first row of projects -->

 
## Shipwrecks in the Chesapeake Bay

I found shipwreck data and a nautical map from NOAA's catalog. I made this map to show all of Shipwrecks
in the Chesapeake Bay by year found. I had to sort through three large data files to get the year's that the shipwrecks
were found in.

I made a gif for all of the years that shipwrecks were found in. I split them up into sections from 1911 - 1955,
1955 - 1975, 1975 - 1990, 1990 - 2004, 2004 - 2017.
I also made two heat maps of where the Shipwrecks and obstructions (pieces of Shipwrecks) where heavily populated at. Last I made a map of where all of
the shipwrecks and obstructions were found, breaking them up into 5 classes with red including the years 1911 - 1955, dark blue including the years 1955 - 1975,
green including the years 1975 - 1990, yellow including the years 1990 - 2004, and light blue including the years 2004 - 2017. I did not include the unknown years
into this map on a count of it would be a lot of data points and be way to confusing for the viewer.


## Shipwrecks Throughout Time in The Chesapeake Bay (Maps)

The map "Shipwrecks Throughout Time In The Chesapeake Bay (By Year Found)" looks like this. (See image below)
I wanted the viewer to see the Chesapeake Bay as a whole to show them that there are in fact a lot of
shipwrecks and obstructions in the bay. I had to use a tool called extract/clip by extract to just get
the points I wanted from the large data files for just the Chesapeake Bay. Once I did that, then I used the
codes (found in the section codes) to sort them out by year found. After I did that then I could take the years found
and brock them up into a graduated by year found which I then broke up into different colors.
Then I had to zoom in on the northern and southern part of the bay and make the points smaller in order for
the viewer to see all of the points and to see what years they were found in.

![shipwrecks](https://github.com/amanda49/amanda49.github.io/blob/master/Shipwrecks_Baltimore_MD.png?raw=true)

The map "Shipwrecks In the Chesapeake Bay" looks like this. (See image below) I wanted the viewer to understand
where the heavily densest parts of the bay were with shipwrecks. I used a tool called merge vector layers for the
two data files that had shipwrecks in them. After I merged them together I then used a tool called
heatmap to figure out where the most densest parts of the bay were in correlation to shipwrecks.

![heat_map_ship_wreck](https://github.com/amanda49/amanda49.github.io/blob/master/Heat_Map_Ship_Wreck.png?raw=true)

The map "Obstructions In the Chesapeake Bay" looks like this. (See image below) I wanted the viewer to understand
where the heavily densest parts of the bay were with obstructions. I used a tool called
heatmap to figure out where the most densest parts of the bay were in correlation to obstructions.

![heat_map_obstructions](https://github.com/amanda49/amanda49.github.io/blob/master/Heat_Map_Obstructions.png?raw=true)

## Gif

 This is a .gif that is broken up by five different time frames to illustrate when shipwrecks and obstructions were
 found throughout the Chesapeake Bay. The shipwrecks are in red and the obstructions are in light blue. The obstructions
 start in the 1920's and end in 2014, while the shipwrecks start in 1911 and end in 2017. Both the shipwrecks and
 obstructions end in the same year, so the next set of years can start and end in the same year.

![ezgif com-resize](https://github.com/amanda49/amanda49.github.io/blob/master/Shipwrecks.gif?raw=true)

## Codes

 I used this code to get the base map into qgis and once I got that I then overlaid the nautical map, which I found from NOAA's catalog, to put on top
 of the base map.
 ````Python
 qgis.utils.iface.addRasterLayer("http://server.arcgisonline.com/arcgis/rest/services/ESRI_Imagery_World_2D/MapServer?f=json&pretty=true","raster")
 ````

 For two of the data files I had to use this code in the field calculator to get the years found:
 ````Python
 concat('19',substr("HISTORY",strpos("HISTORY", '/')+1,2))
 ````

 For the last data file I had to use this code in the field calculator to get the years found:
 ````Python
 left("SORDAT",4)
 ````

This code allows your to change the symbiology of the shipwreck points
to the color red and then allows you to select the year to which you
want to view. For example I picked the year 1997 and this is what happened. (See image below)

````Python
ships = QgsVectorLayer('E:/GIS 486 Project 2/Data/ships.shp','ships')
QgsProject.instance().addMapLayers([ships])

renderer = ships.renderer()
renderer
symbol = renderer.symbol()
symbol.dump()
symbol.setColor(Qt.red)
ships.triggerRepaint()

iface.layerTreeView().refreshLayerSymbology(ships.id())

selection = ships.getFeatures(QgsFeatureRequest().setFilterExpression(u'"YearFound" = 1997'))
ships.selectByIds([s.id() for s in selection])

iface.mapCanvas().zoomToSelected()
````
![code](https://github.com/amanda49/amanda49.github.io/blob/master/code.JPG?raw=true)


