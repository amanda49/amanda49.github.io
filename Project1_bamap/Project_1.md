---
title: Sea Level Rise
feature image: ![project1_feature](https://user-images.githubusercontent.com/42807705/50262822-0cdf5a80-03e1-11e9-8387-ebdebf15aa2b.jpg)
---
<!--This is the first row of projects -->


My project was how water level rise by 10 feet will affect the land coverage (how much
area of land will be lost), population, and buildings that will be lost due to sea level rise.

The database's that were used in this project were:
SHP files, GDBTABLE files, TIF files, GPKG files, and SQLITE files. 
I also made a SQL Query select (Geometry) from real_property.

There was a lot that was involved in this project. For starters I
had to find the water layer, which was from NOAA; https://coast.noaa.gov/slrdata/.
Once I got the data I had to change it over to a vector because it was
in GDBTABLE File format.

The next set of data was provided by my professor, which was the Open
Data Baltimore City data. And the last set of data was from the United States
Census Bureau; https://www.census.gov/geo/maps-data/data/tiger-data.html.

I had to clip the water layers out to only have the Baltimore area show up.
I had to set all of the projects to EPSG: 2893 - NAD83(HARN)/Maryland(ftUS).
I had to use fix geometries a lot in order to get the clip tool to work.
I also used count points in polygon, point on surface tool, and create grid tool
so I could create a hexagonal map. I also, opened up the attribute table and
opened up the field calculator to create a new field in the attribute table.
I used area and sum tool to figure out values, like area (buildings and land), the sum of total area, and
the sum of total population. Having multiply resources of data helped. I also made a 3D map of Baltimore's
elavation and the sea level rise.

### Sea Level Rise

This map shows what Baltimore City would look like if the sea level rised by 10 feet.
I calculated the total area of land that Baltimore City has right now (in 2018). The total
area of land that Baltimore has is 77 miles squared. I calculated the total area of the sea
level rise when it rises by 10 feet. The total area would be 3.5 miles squared. Then calculated
what the total area of land would be after the sea level rised by 10 feet. The total would be 73.7 miles squared.
That is a land cover lost by 3.5 miles squared. That may not seem like a lot, however their are bussiness that would
be affected by this.

![sea level rise](https://user-images.githubusercontent.com/42807705/49679447-5cc13780-fa59-11e8-9e95-21b85ab2c804.png)

### Population in Danger

This map shows the total population in Baltimore City and the population that would be affected by the sea level rise.
I calculated the total population in Baltimore, it is 735,367 people living in this city. I was instructed in seeing
how many people would be in danger by the sea level rise by 10 feet. I only wanted to see who was in danger, so
I clipped the sea level with the population to just end up with the people that would be affected. The total population
that would be affected by the sea level rise of 10 feet would be 83,628.

Compared to the land cover lost by the sea level rise, which is a small area, that is a lot of people that will be
affected by this phenomenon.

![2](https://user-images.githubusercontent.com/42807705/49528930-f8e51600-f882-11e8-97c0-bf1e044959b1.PNG)

### Buildings in Danger

This map shows the all of the buildings that are in Baltimore City and the buildings that would be affected by the
sea level rise. I had to calculate the total area of the buildings and the buildings that would be affected by the
sea level rise to figure out the total area of buildings that would remain after the sea level rised. The total area
of buildings in Baltimore right now is 293,646,093 feet squared. The area of buildings that would be affected by the
sea level rise would by 9,829,641 feet squared. The area buildings that would remain in Baltimore City would be
283,816,452 feet squared. That is a lost of square footage of 9,829,641 feet squared.

I chose to do a hexagonal map to represent the square footage of the buildings. By doing this it makes the map
a lot easier to see which areas of Baltimore have buildings.

![3](https://user-images.githubusercontent.com/42807705/49528932-f8e51600-f882-11e8-900b-aa15e56587e5.PNG)
