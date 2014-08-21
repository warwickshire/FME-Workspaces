How to use
==========
The AddressBase Premium loader is fully documented internally and contains a complete set of parameters allowing full configuration (except for the database credentials; FME can't do them).

Order should be of CSV filetypes.

Open up "RUN ME - FULL - ABP into Oracle - Create.fmw" and read the annotation.

Note that you'll probably have to open the "Oracle Loading" stages and updated the "Joiner transformers" within them to point at the excel/csv files they required. These are included in the "files for load" directory. Similarly the "Stage 1" workspace may need to be reconfigured to point at this directory.


To change database credentials open the following and change as applicable. These contain the writers.

-- Runee - COU - Stage 3 - Oracle Deleting.fmw					[in the SQL_Delete transformer]
-- Runee - COU - Stage 4 - Oracle Loading - INSERT.fmw
-- Runee - FULL - Stage 3 - Oracle Loading - CREATE.fmw


What it does
============

Stages
------

The Full loader runs in three stages. The COU in 4.

Both
Stage 1 - Creates txt files which contain the headers for the fields.
Stage 2 - Splits the supplied CSV file into component parts.

COU Only
Stage 3 - Read the split files and delete anything that's to be updated or deleted.

Stage 4 (COU) / Stage 3 (Full) - Inserts any data that is marked for updating or inserting.

Tables
------

The process creates a database table for every record type. When the load is complete some SQL is run which creates a couple of tables. One table: **OS_ABP_T_BS7666** contains the geographical address.

The other table **OS_ABP_T_DELIVERY_ADDR** contains the delivery address.
These are updated at the end of the update by dropping then reloading. I did try a Materialised View for a while but GIS'es weren't having it.

