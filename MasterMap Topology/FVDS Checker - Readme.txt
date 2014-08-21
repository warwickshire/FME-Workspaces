============================
FVDS Checker
============================
OS MasterMap comes with Feature Validation which allows you to check that your data is good and you don't have extra, missing, or different features. Currently you have to order this at the same time you order your original MasterMap load.

----------------------------
LIMITATIONS
----------------------------
 - RAM Usage - Because of the way that the COU loader works, it basically preloads the entire live dataset's TOIDS into RAM for joining. And then it preloads the entire FVDS too. This results in lots of Massive RAM use for large datasets. If you don't have the RAM, FME will write to disk, but this is significantly slower.

 
 
----------------------------
HOW TO USE
----------------------------

+++++++++++++++++++
Very First Time Use
+++++++++++++++++++
For first time use (if not already set up on a machine). Once set, none of this part should need to be done again.

1) You'll need to set all of the Published Parameters (under "User Parameters"):

	[Source_Oracle_Server] - Your Oracle server name

	[Oracle_username] - The Oracle Username

	[Oracle_password] - The Oracle Password

	[Destination_FAILED_FVDS] - A directory where CSV files contained TOIDS that have failed the FVDS check are placed.


2) If you changed the destination table set, you'll also need to do the following:
	A) SQLCreator - Make sure SQL is pointing to right table set.

3) Continue on to "If already set up" below.


+++++++++++++++++++
If already set up:
+++++++++++++++++++

1) [Source_MasterMap_Data] - Point this published parameter at the directory that has your FVDS GZ files in.
2) Run.
3) Check to see nothing has been written to the Lost Data directory. Anything output to here will still be in the database, but will be symbolised with "Unknown" type.



----------------------------
BENCHMARKS
----------------------------
We've conducted a number of benchmark tests using various sized datasets.

4.3 million features 
RAM Use: ~14GB
Time: ~17mins

28.8million features:
RAM Use: ~3/5ths Physical RAM (so 20GB)
Temp Disk Use: ~25GB
Time: ~4hrs 8mins



----------------------------
----------------------------
----------------------------