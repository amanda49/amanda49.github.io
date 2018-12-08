Part 1
7.5
>>> natural_earth = QgsRasterLayer('Y:/GES 486/lab_4/shapefiles/HYP_HR_SR/HYP_HR_SR.tif', 'Natural Earth')
>>> natural_earth.isValid()
    True
>>> QgsProject.instance().addMapLayer(natural_earth)
    <qgis._core.QgsRasterLayer object at 0x00000153D4930828>
Output:
7.7
1)
>>>wb = iface.addVectorLayer('Y:/GES 486/lab_4/shapefiles/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
2)
>>>wb = iface.addVectorLayer('Y:/GES 486/lab_4/shapefiles/pyqgis3_files/data/world_borders.shp', 'world_borders', 'ogr')
>>>renderer = wb.renderer()
>>>renderer
   <qgis._core.QgsSingleSymbolRenderer object at 0x00000153D4942708>
>>>symbol = renderer.symbol()
>>>symbol.dump()
>>>'FILL SYMBOL (1 layers) color 229,182,54,255'
>>>symbol.setColor(QColor('green'))
>>>wb.triggerRepaint()
>>>symbol.setColor(QColor(0,255,0,175))
>>>wb.triggerRepaint()
3)
>>>wb.triggerRepaint()
>>>layer_tree = iface.layerTreeView()
>>>layer_tree.refreshLayerSymbology(wb.id())
Output:
Part 2
Vector Layer from File Sample
>>>layer = QgsVectorLayer('Y:/GES 486/lab_4/shapefiles/NYC_MUSEUMS_GEO(1)/NYC_MUSEUMS_GEO.shp', 'New York City Museums', 'ogr')
>>>layer.isValid()
   True
>>>QgsProject.instance().addMapLayers([layer])
  [<qgis._core.QgsVectorLayer object at 0x0000017557E89EE8>]
Vector Layer Features
>>>layer = QgsVectorLayer('Y:/GES 486/lab_4/shapefiles/NYC_MUSEUMS_GEO(1)/NYC_MUSEUMS_GEO.shp', 'New York City Museums', 'ogr')
>>>features = layer.getFeatures()
>>>f = next(features)
>>>g = f.geometry()
>>>g.asPoint()
   <QgsPointXY: POINT(-74.01375579573735308 40.70381655004537436)>
Vector Layer Attributes
>>>layer = QgsVectorLayer('Y:/GES 486/lab_4/shapefiles/NYC_MUSEUMS_GEO(1)/NYC_MUSEUMS_GEO.shp', 'New York City Museums', 'ogr')
>>>features = layer.getFeatures()
>>>f = next(features)
>>>f.attributes()
  ['Alexander Hamilton U.S. Custom House', '(212) 514-3700', 'http://www.oldnycustomhouse.gov/', '1 Bowling Grn', NULL, 'New York', 10004.0]
Filtering a layer by geometry
>>>lyrPts = QgsVectorLayer("Y:/GES 486/lab_4/shapefiles/MSCities_Geo_Pts/MSCities_Geo_Pts.shp", "MSCities_Geo_Pts", "ogr")
>>>lyrPts.isValid()
>>>lyrPoly = QgsVectorLayer("Y:/GES 486/lab_4/shapefiles/GIS_CensusTract/GIS_CensusTract_poly.shp", "GIS_CensusTract_poly", "ogr")
>>>lyrPoly.isValid()
>>>QgsProject.instance().addMapLayers([lyrPts,lyrPoly])
>>>ftsPoly = lyrPoly.getFeatures()
>>>for feat in ftsPoly:
    >>>geomPoly = feat.geometry()
    >>>featsPnt = lyrPts.getFeatures(QgsFeatureRequest().setFilterRect(geomPoly.boundingBox()))
>>>for featPnt in featsPnt:
    >>>if featPnt.geometry().within(geomPoly):
        >>>print (featPnt.id())
        >>>lyrpts.select(featPnt.id())
>>>iface.setActiveLayer(lyrPoly)
>>>iface.zoomToActiveLayer()
Output:
Filtering a layer by geomtry (Zoom In)
>>>layer = QgsVectorLayer('Y:/GES 486/lab_4/shapefiles/NYC_MUSEUMS_GEO(1)/NYC_MUSEUMS_GEO.shp', 'Museums', 'ogr')
>>>layer.isValid()
   True
>>>QgsProject.instance().addMapLayers([layer])
   [<qgis._core.QgsVectorLayer object at 0x00000252ED1F9318>]
>>>selection = layer.getFeatures(QgsFeatureRequest().setFilterExpression(u'"ZIP" = 10002'))
>>>layer.selectByIds([s.id() for s in selection])
>>>iface.mapCanvas().zoomToSelected()
Output:
Buffer a feature intermediate
>>>layer = QgsVectorLayer('Y:/GES 486/lab_4/shapefiles/NYC_MUSEUMS_GEO(1)/NYC_MUSEUMS_GEO.shp', 'Museums', 'ogr')
>>>layer.isValid()
   True
>>>QgsProject.instance().addMapLayers([lyr])
   []
>>>fts = lyr.getFeatures()
>>>ft = next(fts)
>>>lyr.selectByIds([ft.id()])
>>>buff = ft.geometry().buffer(.2,8)
>>>buffLyr = QgsVectorLayer('Polygon?crs=EPSG:4326', 'Buffer', 'memory')
>>>pr = buffLyr.dataProvider()
>>>b = QgsFeature()
>>>b.setGeometry(buff)
>>>pr.addFeatures([b])
   (True, [<qgis._core.QgsFeature object at 0x00000252ED1F91F8>])
>>>buffLyr.updateExtents()
>>>buffLyr.setOpacity(.3)
>>>QgsProject.instance().addMapLayers([buffLyr])
   [<qgis._core.QgsVectorLayer object at 0x00000252EEC873A8>]
Output:
Measuring the distance between two points
>>>import qgis.core
>>>lyr = QgsVectorLayer('Y:/GES 486/lab_4/shapefiles/NYC_MUSEUMS_GEO(1)/NYC_MUSEUMS_GEO.shp', 'Museums', 'ogr')
>>>layer.isValid()
>>>fts = lyr.getFeatures()
>>>first = next(fts)
>>>last = next(fts)
>>>for f in fts:
    >>>last = f
>>>d = QgsDistanceArea()
>>>m = d.measureLine(first.geometry().asPoint(),last.geometry().asPoint())
>>>x=d.convertLengthMeasurement(m, 0)
>>>print(x)
   4401.1622240174165
Measuring the distance along a line Sample
>>>import qgis.core
>>>lyr = QgsVectorLayer('Y:/GES 486/lab_4/shapefiles/paths/paths.shp', 'Route', 'ogr')
>>>lyr.isValid()
>>>fts = lyr.getFeatures()
>>>route = next(fts)
>>>d = QgsDistanceArea()
>>>e = QgsEllipse()
>>>m = d.measureLine(route.geometry().asPolyline())
>>>x = d.convertLengthMeasurement(m,0)
>>>print(x)
Calculating the area of a Polygon
>>>import qgis.core
>>>lyr = QgsVectorLayer('Y:/GES 486/lab_4/shapefiles/Mississippi/Mississippi.shp', 'Mississippi', 'ogr')
>>>lyr.isValid()
>>>fts = lyr.getFeatures()
>>>boundary = next(fts)
>>>d = QgsDistanceArea()
>>>m = d.measurePolygon(boundary.geometry().asPolygon())
>>>x = d.convertLengthMeasurement(m, 0)
>>>print(x)
Creating a Spatial Index
>>>lyr = QgsVectorLayer('Y:/GES 486/lab_4/shapefiles/NYC_MUSEUMS_GEO(1)/NYC_MUSEUMS_GEO.shp', 'New York City Museums', 'ogr')
>>>lyr.isValid()
>>>fts = lyr.getFeatures()
>>>first = next(fts)
>>>index = QgsSpatialIndex()
>>>index.insertFeature(first)
>>>for f in fts:
    >>>index.insertFeature(f)
>>>hood = index.nearestNeighbor(first.geomtry().asPoint(), 4)
