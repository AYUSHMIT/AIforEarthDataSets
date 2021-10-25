# Monitoring Trends in Burn Severity (MTBS) Mosaics

## Overview

Annual burn severity mosaics for the continental United States and Alaska.

[Monitoring Trends in Burn Severity](https://www.mtbs.gov/) (MTBS) is an inter-agency program whose goal is to consistently map the burn severity and extent of large fires across the United States from 1984 to the present. This includes all fires 1000 acres or greater in the Western United States and 500 acres or greater in the Eastern United States.

The burn severity mosaics consist of thematic raster images of MTBS burn severity classes for all currently completed MTBS fires for the continental United States, Alaska, Hawaii, and Puerto Rico. Mosaicked burn severity images are compiled annually for each year by US State and the continental United States.  This Azure dataset contains the CONUS and Alaska mosaics.

Source: Monitoring Trends in Burn Severity program (U.S. Geological Survey and USDA Forest Service)

Domain: CONUS and Alaska, 1984-2018

Resolution: 30m


## Storage resources

Data are stored in blobs in the West Europe Azure region, in the following blob folder:

`https://cpdataeuwest.blob.core.windows.net/cpdata/raw/mtbs`

Within that container, data are organized according to:

[region]/30m/severity/[year].tif

`region` is the spatial domain; currently `conus` or `ak`.

`year` is four digit year (e.g. 2017).

Images are stored in cloud optimized GeoTIFF format.

We also provide a read-only SAS (<a href="https://docs.microsoft.com/en-us/azure/storage/common/storage-sas-overview">shared access signature</a>) token to allow access to this data via, e.g., BlobFuse, which allows you to mount blob containers as drives:

`?sv=2019-12-12&si=cpdata-ro&sr=c&sig=tqRGrmdYYa9WYkaPi0wWOD0nalRdNGTZNe97GL2enDA%3D`

Mounting instructions for Linux are [here](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-how-to-mount-container-linux).

Large-scale processing is best performed in the West Europe Azure data center, where the data are stored.  If you are using this data for environmental science applications, consider applying for an [AI for Earth grant](http://aka.ms/ai4egrants) to support your compute requirements.


## Sample code

A complete Python example of accessing and plotting MTBS data is available in the accompanying [sample notebook](https://nbviewer.jupyter.org/github/microsoft/AIforEarthDataSets/blob/main/data/mtbs.ipynb).


## Contact

For questions about this dataset, contact [`aiforearthdatasets@microsoft.com`](mailto:aiforearthdatasets@microsoft.com?subject=mtbs%20question).


## Notices

Microsoft provides this dataset on an "as is" basis.  Microsoft makes no warranties (express or implied), guarantees, or conditions with respect to your use of the dataset.  To the extent permitted under your local law, Microsoft disclaims all liability for any damages or losses - including direct, consequential, special, indirect, incidental, or punitive - resulting from your use of this dataset.  This dataset is provided under the original terms that Microsoft received source data.
