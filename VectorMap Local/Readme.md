How to Use
===========
Designed for loading VectorMap Local from GML files. It does several things:

* Mosaics data together. This gets rid of the unsightly lines between tiles for things like buildings.

* Converts text into line features that are correctly oriented/sized etc; allows for easier rendering.

* Does a *lot* of data clean up. The source data is pretty bad. Mosaicing it together only makes it much much worse.

* Turns point symbols into suitable line symbols. This saves having to style them all up in the GIS (only Colour needs to be done).


You'll need to ensure that the shapefile with the point symbols is correctly pointed to.