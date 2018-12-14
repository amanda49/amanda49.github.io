---
title: Coding
---
<!--This is the first row of projects -->


## Chapter 8
1)
````python
import PyQt5.QtGui
import PyQt5.QtCore
import qgis.utils

wb = iface.addVectorLayer('Y:/GES 486/lab_5/shapefiles/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
wb.isValid()

def load_layer():
   iface.addVectorLayer('Y:/GES 486/lab_5/shapefiles/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')



def change_color():
   active_layer = iface.activeLayer()
   renderer = active_layer.renderer()
   symbol = renderer.symbol()
   symbol.setColor(QColor(Qt.red))
   iface.layerTreeView().refreshLayerSymbology(active_layer.id())


def open_attribute_table():
    iface.showAttributeTable(iface.activeLayer())

load_layer()

renderer = active_layer.renderer()
symbol = renderer.symbol()
symbol.setColor(QColor(Qt.red))
active_layer.triggerRepaint()

iface.showAttributeTable(iface.activeLayer())
````

![script 8 1](https://user-images.githubusercontent.com/42807705/49679243-f38cf480-fa57-11e8-9763-fdc9587e23f1.png)

2)
````Python
import PyQt5.QtGui
import PyQt5.QtCore
import qgis.utils

def load_layer():
    wb = QgsVectorLayer('Y:/GES 486/lab_5/shapefiles/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
    QgsProject.instance().addMapLayer(wb)

def change_color():
    active_layer = wb()
    renderer = layer.renderer()
    symbol = renderer.symbol()
    symbol.setColor(QColor('red'))
    wb.layerTreeView().refreshLayerSymbology(active_layer.id())

load_layer()
````
This one worked, but did not change the color.

````Python
import PyQt5.QtGui
import PyQt5.QtCore
import qgis.utils

def load_layer():
    wb = QgsVectorLayer('Y:/GES 486/lab_5/shapefiles/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
    QgsProject.instance().addMapLayer(wb)

def change_color():
    active_layer = wb()
    renderer = layer.renderer()
    symbol = renderer.symbol()
    symbol.setColor(QColor('#ff0000'))
    wb.layerTreeView().refreshLayerSymbology(active_layer.id())

load_layer()
````
This one worked, it made the map dark red.

````Python
import PyQt5.QtGui
import PyQt5.QtCore
import qgis.utils

def load_layer():
    wb = QgsVectorLayer('Y:/GES 486/lab_5/shapefiles/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
    QgsProject.instance().addMapLayer(wb)

def change_color():
    active_layer = wb()
    renderer = layer.renderer()
    symbol = renderer.symbol()
    symbol.setColor(QColor(255, 0, 0, 255))
    wb.layerTreeView().refreshLayerSymbology(active_layer.id())

load_layer()
````
This one loaded the data, but did not change the color.
````Python
import PyQt5.QtGui
import PyQt5.QtCore
import qgis.utils

def load_layer():
    wb = QgsVectorLayer('Y:/GES 486/lab_5/shapefiles/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
    QgsProject.instance().addMapLayer(wb)

def change_color():
    active_layer = wb()
    renderer = layer.renderer()
    symbol = renderer.symbol()
    symbol.setColor(QColor(Qt.red))
    wb.layerTreeView().refreshLayerSymbology(active_layer.id())

load_layer()
````
This one worked, but did not change the color.

3)
````Python
import PyQt5.QtGui
import PyQt5.QtCore
import qgis.utils

def load_layer():
    wb = QgsVectorLayer('Y:/GES 486/lab_5/shapefiles/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
    QgsProject.instance().addMapLayer(wb)

load_layer()
````
4)
````Python
import PyQt5.QtGui
import PyQt5.QtCore
import qgis.utils

def load_raster():
    raster_lyr = QgsRasterLayer('Y:/GES 486/lab_5/shapefiles/NE2_LR_LC_SR_W_DR/NE2_LR_LC_SR_W_DR/NE2_LR_LC_SR_W_DR.tif', 'NE2_LR_LC_SR_W_DR')
    QgsProject.instance().addMapLayer(raster_lyr)

load_raster()
````
## Chapter 9
1)

![q1 ch9](https://user-images.githubusercontent.com/42807705/49679079-bc6a1380-fa56-11e8-88d5-beecd47c3dc7.PNG)
![q1 ch9 1](https://user-images.githubusercontent.com/42807705/49679080-bc6a1380-fa56-11e8-85a8-fb4f21a20e60.PNG)
![q1 ch9 2](https://user-images.githubusercontent.com/42807705/49679078-bc6a1380-fa56-11e8-8659-dc96c174103f.PNG)

2)
````Python
from qgis.PyQt.QtCore import QVariant

def load_point():
    mem_layer = QgsVectorLayer("Point?crs=epsg:4326&field=id:integer&field=name:string(20)&index=yes", "Roads", "memory")
    QgsProject.instance().addMapLayer(mem_layer)

mem_layer.startEditing()
points = QgsPointXY(-10,61)
feature = QgsFeature()
feature.setGeometry(QgsGeometry.fromPointXY(points))
feature.setAttributes([1, 'QGIS Point'])
mem_layer.addFeature(feature)
mem_layer.commitChanges()

load_point()
````
3)
````Python
from qgis.PyQt.QtCore import QVariant
import qgis.utils

def load_memory_layer():
    mem_layer = QgsVectorLayer("Point?crs=epsg:4326&field=id:integer&field=name:string(20)&index=yes", "Points", "memory")
    QgsProject.instance().addMapLayer(mem_layer)

mem_layer.startEditing()
points = QgsPointXY(10,10)
feature = QgsFeature()
feature.setGeometry(QgsGeometry.fromPointXY(points))
feature.setAttributes([1, 'QGIS Point'])
mem_layer.addFeature(feature)
mem_layer.commitChanges()
settings = QgsPalLayerSettings()
settings.enable = True
settings.fieldName = 'label'
labeling = QgsVectorLayerSimpleLabeling(settings)
labeling.placement = QgsPalLayerSettings.OverPoint
mem_layer.triggerRepaint()

load_memory_layer()
````
This worked, but did not show up over the point.

4)
````Python
from qgis.PyQt.QtCore import QVariant
import qgis.utils
from PyQt5 import QtGui

def load_memory_layer():
    mem_layer = QgsVectorLayer("Point?crs=epsg:4326&field=id:integer&field=name:string(20)&index=yes", "Points", "memory")
    QgsProject.instance().addMapLayer(mem_layer)

mem_layer.startEditing()
points = QgsPointXY(10,10)
feature = QgsFeature()
msg = QInputDialog()
test = "test"
namebox = QInputDialog.getText(msg, test, "Name for feature")
feature.setGeometry(QgsGeometry.fromPointXY(points))
feature.setAttributes([1, namebox[0]])
mem_layer.addFeature(feature)
mem_layer.commitChanges()

load_memory_layer()
````
