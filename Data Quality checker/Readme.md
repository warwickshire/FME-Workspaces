How to use
==========
This workbench contains a full-featured data quality checker that can read from any format FME supports. It creates a report in a number of formats (TAB, CSV, Shape), including spatially indicating where the problem feature is. It's also possible to configure which tests to run.


Inputs
======
Any spatial format that FME supports should be fine. If the generic file reader doesn't do what you want, then put your own reader there instead.
It is advised you use "Prompt and Run Translation" to run the workspace.


Outputs
=======
You can set a destination directory. For every feature type read a set of files will be written. These are:

* Shapefile containing points at all failed locations and an attribute saying why it failed.

* MapInfo TAB file containing points at all failed locations and an attribute saying why it failed.

* CSV with a row every featuring textual description of all errors and Easting and Northings of where they all are.


Tests conducted
===============

Point
-----

* Valid coordinate (OSGB only) 

Checks to ensure that the coordinates are valid OSGB coordinates by simply ensuring there are between 3 and 7 digits.

Line 
----
* Self Intersection 

Use FME's Geometry Validation to detect self-intersections of line features with themselves.


Area (Polygon)
--------------

* OGC Valid Polygon 

Use FME's Geometry Validation to detect a range of issues such as self-intersections, rings, etc etc.

* Overlaps

Detects polygon overlaps within the dataset. Ideal for finding issues with data that's supposed to be topological in nature.
*Caution* This test can be slow with larger datasets.

* Slivers [Experimental!]

Tries to detect slivers between polygons. Ideal for checking topological datasets.
*Caution* This test can be will be slow with larger datasets.


Line & Area 
-----------
These test can be run against both Line and Area (polygon) datasets.

* Duplicate Vertices (exact same location)

Finds any duplicate vertices; i.e. where two vertices are on the same point.

* Vertices too close (within 1m)

Uses the snapper to determine whether there are any other vertices within 1m. Has a high false-positive rate for some reason. (should probably be changed to nearest neighbour).

* Spikes

Tries to identify spikes within the dataset. Uses an angle of 5 degrees.


All 
---
This dataset can be run against any data type.

* Is data in a certain region?

Performs a spatial query to ensure that all features are within a bounding box of your choice. Perfect for finding mis-placed features.


Caveats
===============
There are a few caveats here. Some tests are many tests are very reliable, but some are not.

* Vertices too close (within 1m) - pulls up a lot of false positives.

* Slivers - Due to the nature of the way FME handles the Clipper (it assumes that geometry is "clean"), this can crash FME sometimes. We can't clean the data because that'd defeat the point of the tester. :-)
If FME crashes, it's probably worth re-running and disabling this test.
