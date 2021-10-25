# Landsat 7 Collection 2 Level-2

## Overview

The [Landsat](https://landsat.gsfc.nasa.gov/) program has been imaging the Earth since 1972; it provides a comprehensive, continuous archive of the Earth's surface.

This dataset represents the global archive of Level-2 [Landsat 7](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-7) data from [Landsat Collection 2](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-collection-2); this dataset includes all Landsat 7 images, from 1999 to the present.  Because there is some latency before Level-2 data is available, a rolling window of recent Level-1 data is available as well.  Images are stored in [cloud-optimized GeoTIFF](https://www.cogeo.org/) format.

In 2003, Landsat 7 experienced a hardware failure that resulted in lost pixels.  All images since 2003 have had approximately 22% of their pixels removed; see the <a href="https://www.usgs.gov/faqs/what-landsat-7-etm-slc-data?qt-news_science_products=0#qt-news_science_products">USGS documentation on this issue</a> for more details.

Landsat 7 imagery is currently in preview on Azure; email [`aiforearthdatasets@microsoft.com`](mailto:aiforearthdatasets@microsoft.com?subject=landsat%20question) to request access.


## Storage resources

### Container information

Data are stored in blobs in the West Europe Azure region, in the following blob container:

`https://landsateuwest.blob.core.windows.net/landsat-c2`


### Scene names

Within that container, each scene corresponds to a folder, named according to:

`[level]`/standard/`[sensor]`/`[year]`/`[path]`/`[row]`/[scene name]`

* `[level]` is a processing level ("level-1" or "level-2", always "level-2" for this collection)
* `[sensor]` is one of "mss" (Landsat 1-4), "tm" (Landsat 4-5), "etm" (Landsat 7), or "oli-tirs" (Landsat 8), (always "etm" for this collection, for the Landsat 7 <u>e</u>nhanced <u>t</u>hematic <u>m</u>apper instrument)
* `[year]` is a four-digit year
* `[path]` and `[row]` are three-digit codes representing path/row coordinates in the [Landsat Worldwide Reference System](https://landsat.gsfc.nasa.gov/about/worldwide-reference-system)

`scene name` follows the [Landsat Collection 2 scene name convention](https://www.usgs.gov/faqs/what-naming-convention-landsat-collection-2-level-1-and-level-2-scenes):

`LXSS_LLLL_PPPRRR_YYYYMMDD_yyyymmdd_CC_TX`

* `L` is always "L" for "Landsat"
* `X` is a sensor identifier ("C" for OLI/TIRS combined, "O" for OLI-only, "T" for TIRS-only, "E" for ETM+, "T" for TM, or "M" for MSS)
* `SS` is a satellite identifier ("01", "02", "03", "04", "05", "07", or "08")
* `LLLL` is a [processing correction level](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-levels-processing) (L1TP/L1GT/L1GS for level-1 data, L2SP/L2SR for level-2 data)
* `PPP` is a [WRS](https://landsat.gsfc.nasa.gov/about/worldwide-reference-system) path
* `RRR` is a [WRS](https://landsat.gsfc.nasa.gov/about/worldwide-reference-system) row
* `YYYYMMDD` is the acquisition year, month, day
* `yyyymmdd` is the processing year, month, day
* `CC` is the collection number (always "02" in this dataset)
* `TX`is the [collection category](https://www.usgs.gov/media/videos/landsat-collections-what-are-tiers) ("RT" for real-time, "T1" for tier 1, or "T2" for tier 2)

Putting that all together, a complete scene folder for a Landsat 7 image from February 16, 2020 looks like:

`https://landsateuwest.blob.core.windows.net/landsat-c2/level-2/standard/etm/2020/011/021/LE07_L2SP_011021_20200216_20200822_02_T2/`

### Landsat 7 file names

#### Landsat 7 image files

Within each scene, Landsat 7 files follow the [Landsat 7 Collection 2 Level 2 specification](https://www.usgs.gov/media/files/landsat-7-etm-collection-2-level-2-data-format-control-book); see the specification for complete documentation of both data and metadata.

This section will provide a short summary of the files within each scene folder.  All filenames are prefixed with the scene ID.

Listing *.tif will enumerate all images, with suffixes indicating bands according to the following:

* `B1`: Band 1 Visible (0.45-0.52 µm) 30m
* `B2`: Band 2 Visible (0.52-0.60 µm) 30m
* `B3`: Band 3 Visible (0.63-0.69 µm) 30m
* `B4`: Band 4 Near infrared (0.77-0.90 µm) 30m
* `B5`: Band 5 Short-wave infrared (1.55-1.75 µm) 30m
* `B6`: Band 6 Thermal (10.4-12.5 um) 30m
* `B7`: Band 7 Mid infrared (2.08-2.35 µm) 30m
* `B8`: Band 8 Panchromatic (PAN) (0.52-0.9 µm) 15m (level-1 data only)

For example, the band 2 image in the example scene above is at:

`https://landsateuwest.blob.core.windows.net/landsat-c2/level-2/standard/etm/2020/011/021/LE07_L2SP_011021_20200216_20200822_02_T2/LE07_L2SP_011021_20200216_20200822_02_T2_SR_B2.TIF`

Level-2 files end with "_SR_B[N]", indicating "surface reflectance".

Landsat 7 Level-2 scenes include the following derived images:

* `[sceneID]_ST_TRAD.tif`: thermal image
* `[sceneID]_ST_URAD.tif`: upwelled radiance image
* `[sceneID]_ST_ATRAN.tif`: atmospheric transmission image
* `[sceneID]_ST_CDIST.tif`: distance (in km) from each pixel to the nearest cloud pixel
* `[sceneID]_ST_DRAD.tif`: downwelled radiance image
* `[sceneID]_ST_EMIS.tif`: emissivity image
* `[sceneID]_ST_EMSD.tif`: emissivity standard deviation
* `[sceneID]_SR_ATMOS_OPACITY.tif`: atmospheric opacity estimates

#### Landsat 7 metadata files

* `[sceneID]_MTL.xml`: scene metadata file, in .xml format.  The metadata file includes, among other things, geometry information, a cloud cover percentage, information about sensor saturation, and radiance/reflectance calibration information.
* `[sceneID]_MTL.txt`: the same information in .txt format
* `[sceneID]_MTL.json`: the same information in .json format (level-2 only)
* `[sceneID]_ANG.txt`: [angular coefficients file](https://www.usgs.gov/faqs/what-landsat-collections-angle-coefficient-file-and-how-it-used?qt-news_science_products=0#), which allow users to compute solar and sensor viewing angles on a per-pixel basis

#### Landsat 7 quality assessment files

* `[sceneID]_QA_PIXEL.tif`: [quality assessment band](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-collection-2-quality-assessment-bands)
* `[sceneID]_QA_RADSAT.tif`: [saturation quality assessment image](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-collection-2-quality-assessment-bands), indicating which sensors were saturated on a per-pixel basis
* `[sceneID]_ST_QA.tif`: [quality assessment band](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-collection-2-quality-assessment-bands) for the surface temperature products

#### Landsat 7 thumbnails

* `[sceneID]_thumb_large.jpeg`: large RGB thumbnail
* `[sceneID]_thumb_small.jpeg`: small RGB thumbnail


## Sample code

A complete Python example of accessing and plotting Landsat data - using the NASA CMR API to query for scenes of interest - is available in the accompanying [sample notebook](https://nbviewer.jupyter.org/github/microsoft/AIforEarthDataSets/blob/main/data/landsat-7.ipynb).


## Region information

Large-scale processing is best performed in the West Europe Azure region, where the images are stored.  If you are using Landsat data for environmental science applications, consider applying for an [AI for Earth grant](http://aka.ms/ai4egrants) to support your compute requirements.


## Pretty picture

<img src="https://ai4edatasetspublicassets.blob.core.windows.net/assets/aod_images/landsat-7_thumb_800w.png" style="width:500px;"><br/><span style='font-size:80%'>Natural-color rendering (Landsat 7 bands 3/2/1) of an area near Auckland, New Zealand, carefully cropped to avoid scan line corrector failure issues that make thumbnails less delightful.</span>

## Pretty picture, with 22% of its pixels missing

<img src="https://ai4edatasetspublicassets.blob.core.windows.net/assets/aod_images/landsat-7_slc_failure_800w.png" style="width=500px;"><br/><span style='font-size:80%'>The area from which the above image was cropped, showing the SLC failure issue.</span>


## Contact

For questions about this dataset, contact [`aiforearthdatasets@microsoft.com`](mailto:aiforearthdatasets@microsoft.com?subject=landsat%20question).


## Notices

Microsoft provides this dataset on an "as is" basis.  Microsoft makes no warranties (express or implied), guarantees, or conditions with respect to your use of the dataset.  To the extent permitted under your local law, Microsoft disclaims all liability for any damages or losses - including direct, consequential, special, indirect, incidental, or punitive - resulting from your use of this dataset.  This dataset is provided under the original terms that Microsoft received source data.

