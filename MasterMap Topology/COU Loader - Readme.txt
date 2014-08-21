============================
COU LOADER
============================


WARNING:
DO NOT STOP THIS LOADER MID-LOAD (only applies to COU loader). If you have to, see the bit at the bottom, "IF IT ALL GOES A BIT WRONG".


----------------------------
LIMITATIONS
----------------------------
 - See also, Full Supply Loader limitions (those are shared with this one, but this one has a few extra's).
 - RAM Usage - Because of the way that the COU loader works, it basically preloads the entire live dataset's TOIDS into RAM for joining. This results in lots of RAM use for large datasets. If you don't have the RAM, FME will write to disk, but this is significantly slower.
 - Only one COU loader at a time should be run. The temporary tables it creates in the database for deletions are generically named.

----------------------------
HOW TO USE
----------------------------

+++++++++++++++++++
Very First Time Use
+++++++++++++++++++
For first time use (if not already set up on a machine). Once set, none of this part should need to be done again.

1) You'll need to set all of the Published Parameters (under "User Parameters"):

	[Source_Symbols_Shape] - Point at the directory with the shapefile symbols in ( /Symbols and styles/ )

	[Joiner_Source_Styles] - The source of the styles to be joined to the data. This is supplied in: /Symbols and styles/osmmStyle_names_join_table.csv 

	[Destination_Oracle_Server] - Your Oracle server name

	[Oracle_username] - The Oracle Username

	[Oracle_password] - The Oracle Password

	[Destination_Lost_Data] - A directory where "lost data" can be placed (this is data that doesn't merge properly because of missing styles).


2) If you changed the destination table set, you'll also need to do the following:
	A) SQL_Delete - Make sure SQL is pointing to right table set
	B) SQL_GetMax_IDs - Make sure SQL is pointing to right table set
	C) Joiner_2 - Make sure SQL is pointing to right table set
	D) Ensure Oracle Writers are pointing to desired tables

3) Continue on to "If already set up" below.


+++++++++++++++++++
If already set up:
+++++++++++++++++++

1) [Source_MasterMap_Data] - Point this published parameter at the directory that has your MasterMap COU GZ files in.
2) Run.
3) Check to see nothing has been written to the Lost Data directory. Anything output to here will still be in the database, but will be symbolised with "Unknown" type.



----------------------------
IF IT ALL GOES A BIT WRONG
----------------------------
Because of the way the COU loader works, if something goes wrong, or you stop it during mid load, there can be some tables left in the database. You'll need to manually delete these before running it again.
These tables are created by the loader to facilitate deleting "departedfeatures" and the like.

The following tables will need to be dropped, although not all of them will necessarily exist:

OS_MM_PURGE_ID
OS_MM_BL_PURGE
OS_MM_CS_PURGE
OS_MM_CT_PURGE
OS_MM_TA_PURGE
OS_MM_TL_PURGE
OS_MM_TP_PURGE


----------------------------
BENCHMARKS
----------------------------
We've conducted a number of benchmark tests using various sized datasets.

22 COUs against 18,797 features
RAM Use: Negligible
Time: ~12s

2345 COUs for 194,476 features
Time: < 1 min
RAM use: Negligible

13,356 COUs against 4.3 million features (Warwickshire county)
RAM Use: ~3GB
Time: ~5 mins

35,085 COUs against 28.8 million features (Warwickshire county + 20km buffer)
RAM Use: ~20GB (possibly more, but written to disk by FME)
Time: ~38mins



----------------------------
----------------------------
----------------------------