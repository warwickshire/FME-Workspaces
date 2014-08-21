Release 1.0
Released by Warwickshire County Council.

----------------------------
DESCRIPTION
----------------------------
This set of FME workspaces loads Ordnance Survey supplied MasterMap data (in .gml or zipped .gz format) into an Oracle database.
We developed this internally to save us having to use a vendor solution that was costing us several £thousand a year.

There are three FME workspaces:
* Full Supply loader - For a completely new supply of OSMM data.
* COU loader - For loading a Change Only Update. Should only be used for data that was originall loaded with the above Full Supply loader.
* FVDS checker - Feature Validation Service - Allows validation of the dataset. Again, only for data loaded with either the Full Supply or COU loaders supplied.

----------------------------
WHAT THE LOADER DOES
----------------------------
This is a full-featured loader so it doesn't pretty much everything needed to get the data easily displayable in a GIS.

Specifically it:
 - Joins attribute information for styling from a seperate shapefile to the data (OSMMSTYLE_NAME attribute column).
 - Also joins MapInfo style information to the data and places that into the MI_STYLE column (So MapInfo auto styles it).
 - Converts Topographic Point and Cartographic Symbol points into correctly positioned and oriented line symbols of the right type.
 - Converts Cartographic Text into a correctly placed and oriented line that runs through the middle of the text.
 - Concatenates the Change History of a feature into one single string.
 - Only keeps relevant attributes for each feature type.
 - MI_PRINX is used as the (not-autoincrementing) primary key for the database (useful for MapInfo and ArcSDE).
 - Builds spatial indexes for the spatial data.
 - Write spatial data to a column called SDO_GEOMETRY.

----------------------------
MISC
----------------------------
We release this as a public service to our fellow public sector bodies, but please be aware it comes with no warranty, or support etc.
That said, we do welcome feedback, comments, and will try and answer questions about the workspace if you have any. Please contact: GIS@warwickshire.gov.uk

The output will be auto styled in MapInfo. Courtesy of the OSMMSTLYE_NAME column it can easily be styled in other GIS software. We've released QGIS styles that use this column, and these can be accessed from here: http://hub.qgis.org/wiki/quantum-gis/OS_Styles






----------------------------
USAGE
----------------------------
As can be seen from the benchmarks in the applicable readme files, its best used for subsets of OSMM. We're fairly sure it could load the entire OSMM dataset, but it would take a long time and a lot of RAM.

There's no need to use the COU or FVDS workspaces if you don't want that functionality. Its quite possible to just do a complete load of OSMM data every few months as required.


The default tables that data will be loaded to are:

	OS_MM_BOUNDARYLINE
	OS_MM_CARTOGRAPHIC_SYMBOL
	OS_MM_CARTOGRAPHIC_TEXT
	OS_MM_TOPOGRAPHIC_AREA
	OS_MM_TOPOGRAPHIC_LINE
	OS_MM_TOPOGRAPHIC_POINT
	
These can be changed of course, but for the sake of ease of use, its probably best to leave them as is.

These loaders require FME 2012 SP2 or later. Ideally 64bit if you're going to use large datasets and have more than 4GB of RAM on the machine.


***************
IMPORTANT
***************
Your MasterMap order *must* be for Non Geographically chunked data. It doesn't matter if you go for 10MB, 30MB or 50MB chunks, but it must be "GML non geo chunk" as the order page puts it.



----------------------------
OTHER OUTPUT FORMATS
----------------------------
While this workspace is currently designed for writing to Oracle, there's no reason it can't be changed to write to other output formats, either databases (PostGIS, MS SQL, SpatialLite, etc.), or regular files (shapefile, TAB file, etc.). We did convert the Full Loader to SQLite easily, however FME has a bug with SQLite handling that means the COU can't be converted into that format.

Full Supply loader - Converting this one should be easy. Just change the writers.
COU loader - Much of what this does is directly done by the database itself. Some of the SQL may be Oracle specific so would have to be changed, as well as the writers of course. We're not sure this could be converted to non-database formats.
FVDS checker - Just changing the SQLCreator should be sufficient. Or replace with a regular reader for a regular file probably.





----------------------------
   LICENCE
----------------------------
Copyright 2012, Warwickshire County Council.

Released under the Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported license
We waive the NonCommercial limitation for all PSMA and OSMA members.

We release this as a public service to our fellow public sector bodies and it comes with no warranty, or support etc.