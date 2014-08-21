Raster Loaders Loader
=====================

This directory contains a number of workspaces for raster loading. They're optimised to allow easy loading of Ordnance Survey data; when configured properly an update of all OS raster products can be done with just a few minutes of operater time.


Inputs
------

The inputs are expected to be directories filled with tiled raster products, straight from the OS.

Outputs
-------
This workspace can output in up to four file types (JP2, GeoTiff, ECW and IMG), and for any filetype it can also create a Black and White image or Colour.

Components
----------
There are a number of components to this process, each doing something different. Not all parts have to be run, it depends what the desired output it.

* _1 _ OS_Raster_Creator_RUNNER.fmw

This workspaces is the primary converter. Set up all of the transformers that are inside the "Configure here" bookmark. Each raster type can have the input directory configured, along with the desired product name, whether mosaicing needs to occur, and what output formats are needed. You'll need to look in the **OS_Raster_Ultimate_Processor** for an idea of how to set the output formats. You should only need to configure it once for your holdings; thereafter new loads just require you press Play.

* _2 - GDAL_process GeoTiffs - tiled-pyramided - Runner.fmw

Once stage 1 has been run, run this workspace if you've created GeoTiffs. This workspace will create internal overviews (pyramids), and tiles within any of the rasters. It does this by running **GDAL_process GeoTiffs.fmw**. This makes the GeoTiffs much more responsive.

* _3 - GDAL_process_GeoTiffs - TMS - Runner.fmw

This final loader is only required if you wish to create fixed resolution rasters for use within a TMS. These give a much prettier look than on-the-fly interpolated rasters. As with loader 1, you'll need to configure the workspace the first time you run it for your area/needs/resolutions etc. This workspace runs **GDAL_process GeoTiffs for TMS.fmw**

* GDAL_process GeoTiffs for TMS.fmw

A very simple workspace that calls a local install of GDAL (needs to be configured) which uses gdalwaro to create fixed resolution images for use with a TMS. Because they're only designed to be viewed at once resolution they don't have pyramids/overviews, although they are tiled.

* GDAL_process GeoTiffs.fmw

Processes GeoTiffs, adding the right number of Overviews/pyramids, and tiling as required.

* OS_Raster_Ultimate_Processor.fmw

This is the stand alone loader **you should use if you only one to do one at a time manually**. Just use "Prompt and Run Translation.". Point it toa  directory filled with TIF's, doesn't have to be used just for OS rasters. It has a considerable number of options/capabilities:

* Colour / Black and white for all outputs
* Outputs in JP2, GeoTiff, ECW, IMG formats
* Boundbox can be specified; input raster tiles are only used if within this box.
* Whether to mosaic or not.
* Output filename

