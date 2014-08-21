FME-Workbenches
===============

A collection of FME workbenches created by Warwickshire County Council for loading data and data quality checking. There are a selection of different workspaces.

Ordnance Survey Vector Products
-------------------------------
There are a number of workspaces for loading OS vector datasets, almost all are designed for an Oracle database but can be easily changed to any other sort of writer.

* AddressBase Premium
* MasterMap Topology Layers
* Meridian 2
* Terrain 50
* VectorMap District
* VectorMap Local

In the case of the *MasterMap* COU loader, there may be considerably more effort required to convert it to another writer as it uses a significant amount of SQL which may be SQL specific. Same for the *AddressBase Premium* loaders.


Ordnance Survey Rasters
-----------------------
Some generic loaders have been created for OS Raster products, though they can be used for any raster dataset. There are also some specific loaders which use the generic ones to simplify data creation/management. An update of an entire suite of OS raster products can be done with just a few minutes of operator time.


Data quality Checkers
---------------------
There are a couple of FME workspaces which are designed for data quality checking.

Misc
----
Miscelaneous workspaces.



Caveats
-------

* Everything is currently configured to output as British National Grid, but this can be changed in the usual FME way if required.
* Not everything is set to a parameter that should be. So you may need to delve a little to configure stuff. This is because the workspaces weren't created with the original intention of releasing them.
* Most of them will required at least FME 2014 SP2 although may work in earlier versions anyway.



Contact
=======

To contact the Corporate GIS team about these workspaces, email:
gis@warwickshire.gov.uk
Note that WCC don't offer any form of support for these.

More information about WCC's public Corporate GIS services can be found here:
http://www.warwickshire.gov.uk/gis


About
=====
Initial release: 2014-08-19

Created by Jonathan Moules,
Corporate GIS,
Warwickshire County Council
