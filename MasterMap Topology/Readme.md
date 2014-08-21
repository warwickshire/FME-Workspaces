About
==========

These FME workspaces were created to load Ordnance Survey MasterMap (OSMM).
All loaders require data be suplied in a NON-GEOGRAPHICAL format. File-size is irrelevent.

There are a number of workspaces and each is self-documented.
There are three types of OSMM Loader:

* Full Supply

* COU

* FVDS


Fully Supply
------------

This workspaces loads a Full support of OS MasterMap to Oracle. It requires minimal significant resources
If a Topographic Symbol or Cartographic Symbol doesn't match one of the symbols in the dataset, or if there isn't a style for any specified in any dataset, these will be outputted to a CSV file.



COU
------------
Loads a Change Only Update (COU) against the database. Deletes old features as well as "modified" ones. Then writes "modified" features and new ones.
It doesn't matter if you run it twice and probably not if you run an older COU after a newer one, but these things are advised against.

Resource usage can be very high for RAM due to the way it matches changes.


********************
***     FVDS     ***
********************
The Feature Validation Data Set (FVDS) is used to confirm that a dataset as held in the database is current and valid.
Just look at the FME workspace when its finished and make sure nothing went the wrong way. If it did it will be in a CSV file in the relevant directory.
Note: This is a massive RAM hog, but it shouldn't need running regularly.