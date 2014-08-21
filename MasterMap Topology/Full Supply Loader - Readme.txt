============================
FULL SUPPLY LOADER
============================

----------------------------
LIMITATIONS
----------------------------
 - OS Styling - While Warwickshire is a large county, we don't have all land types that the OS recognises. This means that there may not be OS Stylings in the CSV file for certain DescriptiveTerm combinations. They'll be given an "UnknownStyle" type and a copy will be output into the Lost Data directory.
 - RAM Usage - Because the conversion of Topographic Point and Cartographic Symbol uses the FeatureMerger, which is a grouping transformer, these feature types are stored in RAM until they've all been loaded resulting in quite high RAM usage for very large loads (i.e. 30 million features uses 4GB of RAM).


***************
IMPORTANT
***************
Your MasterMap order *must* be for Non Geographically chunked data. It doesn't matter if you go for 10MB, 30MB or 50MB chunks, but it must be "GML non geo chunk" as the order page puts it.


----------------------------
HOW TO USE
----------------------------

+++++++++++++++++++
Very First Time Use
+++++++++++++++++++
For first time use (if not already set up on a machine). Once set, none of this part should need to be done again.

1) You'll need to set all of the Published Parameters (under "User Parameters"):

	[Source_Symbols_Shape] - Point at the directory with the shapefile symbols in ( /Symbols and styles/ ), or the two shapefiles themselves.

	[Joiner_Source_Styles] - The source of the styles to be joined to the data. This is supplied in: /Symbols and styles/osmmStyle_names_join_table.csv 

	[Destination_Oracle_Server] - Your Oracle server name

	[Oracle_username] - The Oracle Username

	[Oracle_password] - The Oracle Password

	[Destination_Lost_Data] - A directory where "lost data" can be placed (this is data that doesn't merge properly because of missing styles).

2) (Optional) In the Oracle writers, set the Minimum X Coordinate, Minimum Y Coordinate, Maximum X Coordinate, Maximum Y Coordinate. These default to the entire UK, but its best to bound your data more closely than that. If the bounds you give are smaller than the actual data, you'll get very odd (read: bad) results.
These can be done with the published parameters (which updates all 6 writers):
	[oracle_min_x]
	[oracle_min_y]
	[oracle_max_x]
	[oracle_max_y]

3) (Optional) Change the Oracle Writer to create the desired database tables (i.e. the output table names) or just leave them as the defaults (leaving them is preferred if you're going to use the supplied COU loader and/or FVDS checker).

4) Continue on to "If already set up" directly below.


+++++++++++++++++++
If already set up:
+++++++++++++++++++

1) [Source_MasterMap_Data] - Using the "advanced editor" Point this published parameter at the directory that has your Full Supply of MasterMap GZ files in.
2) Run.
3) Check to see nothing has been written to the Lost Data directory. Anything output to here will still be in the database, but will be symbolised with an "Unknown" type.


----------------------------
IF IT ALL GOES A BIT WRONG
----------------------------
If you have to stop the workspace mid-run or it breaks, you can just start it again with no problems. The workspace is set to drop the tables if they exist already.


----------------------------
BENCHMARKS
----------------------------
We've conducted a number of benchmark tests using various sized datasets. Note that the full OS MasterMap dataset is about 500 million features; we've not tried that.

18,797 features:
Time: ~50 secs

194,476 features:
Time: ~7.5 mins

4.3 million features (Warwickshire County)
Time: ~4hrs

28.8 million features (Warwickshire County + 20km buffer; includes much of the West Midlands conurbation)
Time: ~3 days
RAM: ~4GB

While this workspace can be converted to use multiple processors/Cores, in our experience this ends up killing the Oracle database and making the workspace workflow much more complicated. As such, it only uses one CPU Core.

