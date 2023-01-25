# National Water Model

## Overview

The National Water Model (NWM) is a hydrologic modelling framework that simulates observed and forecast streamflow over the entire continental United States (CONUS), Hawaii, and Puerto Rico. The NWM simulates the water cycle with mathematical representations of the different processes and how they fit together. This complex representation of physical processes such as snowmelt and infiltration and movement of water through the soil layers varies significantly with changing elevations, soils, vegetation types and a host of other variables. Additionally, extreme variability in precipitation over short distances and times can cause the response on rivers and streams to change very quickly. Overall, the process is so complex that to simulate it with a mathematical model means that it needs a very high powered computer or supercomputer in order to run in the time frame needed to support decision makers when flooding is threatened.

## Storage Resources

The files are available from the Azure Blob Storage Container at `https://noaanwm.blob.core.windows.net/nwm`. This storage container is in Azure's East US region. Users wishing to perform large-scale processing on the data should also locate their compute in Azure's East US region. All data files are NetCDF4 file format.

The files vary along several facets. Each filename within the container will start with

```
nwm.YYYYMMDD/
```

where `YYYY` is the 4-digest year, `MM` is the two-diget month, and `DD` is the two diget day. Within that day's directory are a set of directories combining various analyses, forecast configurations, and regions.

## Data coverage areas and output variations

Data products may be available for Hawaii and Puerto Rico. This is indicated below for each product.

The data for Hawaii follows the same file name pattern, but have a prefix of `nwm.{YYYYMMDD}/{product}_hawaii/` and files are suffixed with `hawaii.nc` instead of `conus.nc`. For example, the NWM Analysis and Assimilation product for Hawaii has the prefix `nwm.{YYYYMMDD}/analysis_assim_hawaii/nwm.t{CC}z.analysis_assim`.

The data for Puerto Rico follows the same file name pattern, but have a prefix of `nwm.{YYYYMMDD}/{product}_puertorico/` and files are suffixed with `puertorico.nc` instead of `conus.nc`. For example, the NWM Analysis and Assimilation product for Puerto Rico has the prefix `nwm.{YYYYMMDD}/analysis_assim_puertorico/nwm.t{CC}z.analysis_assim`.

In addition, several channel outputs have separate open loop companion configuration, labeled "no_da", which is the same as the respective normal configuration but does not have assimilation data applied. These products are described indicated below as separate entries.

There is also "Extended" versions of the Analysis Assimilation products, including "no_da" products. These filenames follow the same patterns as the non-extended product, but with `_extend` suffixed to the product name. For example: `nwm.20210906/analysis_assim_extend/nwm.t16z.analysis_assim_extend.channel_rt.tm00.conus.nc`

### NWM Analysis and Assimilation

**Analysis and Assimilation** data for the CONUS, Hawaii and Puerto Rico. The files for CONUS begins with the prefix `nwm.{YYYYMMDD}/analysis_assim/nwm.t{CC}z.analysis_assim` where

* `YYYY` is the 4-digest year
* `MM` is the two-digit month
* `DD` is the two digit day
* `CC` is the model cycle runtime (i.e. 00, 06, 12, 18)
* `PP` is the model lookback period (i.e. 00, 01, 02)
* `FFF` is the forecast hour (i.e. 000, 006, 012, 018, etc)
* `MEM` is the forecast ensemble member (1-4 for long-range, 1-7 for medium-range)

|         Description          |                   Filename Pattern                   |                                                        Example                                                         |
| ---------------------------- | ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Point-type Channel Routing   | `{prefix}.analysis_assim.channel_rt.tm{PP}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/analysis_assim/nwm.t00z.analysis_assim.channel_rt.tm00.conus.nc |
| 1km gridded Land Output      | `{prefix}.land.tm{PP}.conus.nc`                      | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/analysis_assim/nwm.t00z.analysis_assim.land.tm00.conus.nc       |
| Point-type Reservoir Output  | `{prefix}.reservoir.tm{PP}.conus.nc`                 | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/analysis_assim/nwm.t00z.analysis_assim.reservoir.tm00.conus.nc  |
| 250m gridded Terrain Routing | `{prefix}.terrain_rt.tm{PP}.conus.nc`                | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/analysis_assim/nwm.t00z.analysis_assim.terrain_rt.tm00.conus.nc |

Analysis and Assimilation data is available for the Continental United States, Hawaii and Puerto Rico.

**Analysis and Assimilation Long** data for the Continental United States. Each file begins with the prefix `nwm.{YYYYMMDD}/analysis_assimi_long/nwm.t{CC}z.analysis_assim_long`, using similar notation as above.

|         Description         |           Filename Pattern            |                                                             Example                                                              |
| --------------------------- | ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Point-type Channel Routing  | `{prefix}.channel_rt.tm{PP}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/analysis_assim_long/nwm.t00z.analysis_assim_long.channel_rt.tm00.conus.nc |
| 1km gridded Land Output     | `{prefix}.land.tm{PP}.conus.nc`       | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/analysis_assim_long/nwm.t00z.analysis_assim_long.land.tm00.conus.nc       |
| Point-type Reservoir Output | `{prefix}.reservoir.tm{PP}.conus.nc`  | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/analysis_assim_long/nwm.t00z.analysis_assim_long.reservoir.tm00.conus.nc  |

Analysis and Assimilation Long data is available only for the Continental United States.

**Analysis and Assimilation Forcing** data for the Continental United States. Each file begins with the prefix `nwm.{YYYYMMDD}/forcing_analysis_assimi/nwm.t{CC}z.analysis_assim`, using similar notation as above.

|       Description        |          Filename Pattern          |                                                           Example                                                           |
| ------------------------ | ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| 1km Gridded Forcing Data | `{prefix}.forcing.tm{PP}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/forcing_analysis_assim/nwm.t00z.analysis_assim.forcing.tm00.conus.nc |

Likewise for Hawaii and Puerto Rico.

**Analysis and Assimilation (No DA)** data for the Continental United States, Hawaii, and Puerto Rico. Each file begins with the prefix `nwm.{YYYYMMDD}/analysis_assimi_no_da/nwm.t{CC}z.analysis_assim_no_da`, using similar notation as above.

|             Description             |           Filename Pattern            |                                                              Example                                                               |
| ----------------------------------- | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Point-type Channel Routing  (No DA) | `{prefix}.channel_rt.tm{PP}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/analysis_assim_no_da/nwm.t00z.analysis_assim_no_da.channel_rt.tm00.conus.nc |

Analysis and Assimilation (No DA) data is available for the Continental United States, Hawaii and Puerto Rico.

**Analysis and Assimilation Long (No DA)** data for the Continental United States. Each file begins with the prefix `nwm.{YYYYMMDD}/analysis_assimi_long_no_da/nwm.t{CC}z.analysis_assim_long_no_da`, using similar notation as above.

|             Description             |           Filename Pattern            |                                                                   Example                                                                    |
| ----------------------------------- | ------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Point-type Channel Routing  (No DA) | `{prefix}.channel_rt.tm{PP}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/analysis_assim_long_no_da/nwm.t00z.analysis_assim_long_no_da.channel_rt.tm00.conus.nc |

Analysis and Assimilation Long (No DA) data is available only for the Continental United States.

### NWM Short Range

**Short range forecast** data for the Continental United States, Hawaii, and Puerto Rico. Each file begins with the prefix `nwm.{YYYYMMDD}/short_range/nwm.t{CC}z.short_range`, using similar notation as above.

|         Description          |           Filename Pattern            |                                                     Example                                                      |
| ---------------------------- | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Point-type Channel Routing   | `{prefix}.channel_rt.f{FFF}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/short_range/nwm.t00z.short_range.channel_rt.f001.conus.nc |
| 1km gridded Land Output      | `{prefix}.land.f{FFF}.conus.nc`       | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/short_range/nwm.t00z.short_range.land.f001.conus.nc       |
| Point-type Reservoir Output  | `{prefix}.reservoir.f{FFF}.conus.nc`  | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/short_range/nwm.t00z.short_range.reservoir.f001.conus.nc  |
| 250m gridded Terrain Routing | `{prefix}.terrain_rt.f{FFF}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/short_range/nwm.t00z.short_range.terrain_rt.f001.conus.nc |

Analysis and Assimilation (No DA) data is available for the Continental United States, Hawaii and Puerto Rico.

**Short Range Forcing** data for the Continental United States, Hawaii, and Puerto Rico. Each file begins with the prefix `nwm.{YYYYMMDD}/forcing_short_range/nwm.t{CC}z.short_range`, using similar notation as above.

|       Description        |          Filename Pattern          |                                                        Example                                                        |
| ------------------------ | ---------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 1km Gridded Forcing Data | `{prefix}.forcing.f{FFF}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/forcing_short_range/nwm.t00z.short_range.forcing.f001.conus.nc |

Likewise for Hawaii and Puerto Rico.

Note that Hawaii and Puerto Rico also include **Short Range NO-DA** data.

### NWM Medium Range

**Medium range forecast** data for the Continental United States. Each file begins with the prefix `nwm.{YYYYMMDD}/medium_range/nwm.t{CC}z.medium_range_mem{MEM}`, using similar notation as above (`{MEM}` refers to the ensemble member).

|         Description          |              Filename Pattern               |                                                          Example                                                          |
| ---------------------------- | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Point-type Channel Routing   | `{prefix}.channel_rt_{MEM}.f{FFF}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/medium_range_mem1/nwm.t00z.medium_range.channel_rt_1.f001.conus.nc |
| 1km gridded Land Output      | `{prefix}.land_{MEM}.f{FFF}.conus.nc`       | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/medium_range_mem1/nwm.t00z.medium_range.land_1.f003.conus.nc       |
| Point-type Reservoir Output  | `{prefix}.reservoir_{MEM}.f{FFF}.conus.nc`  | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/medium_range_mem1/nwm.t00z.medium_range.reservoir_1.f001.conus.nc  |
| 250m gridded Terrain Routing | `{prefix}.terrain_rt_{MEM}.f{FFF}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/medium_range_mem1/nwm.t00z.medium_range.terrain_rt_1.f003.conus.nc |

Medium-range forecast data are only available for the Continental United States.

**Medium Range Forcing** data for the Continental United States. Each file begins with the prefix `nwm.{YYYYMMDD}/forcing_medium_range/nwm.t{CC}z.medium_range`, using similar notation as above.

|       Description        |          Filename Pattern          |                                                         Example                                                         |
| ------------------------ | ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| 1km Gridded Forcing Data | `{prefix}.forcing.f{FFF}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/forcing_medium_range/nwm.t00z.medium_range.forcing.f001.conus.nc |

Medium-range forcing data are only available for the Continental United States.

### NWM Long Range

**Long-range forecasts** are available for the Continental United States. Each file begins with the prefix `nwm.{YYYYMMDD}/long_range/nwm.t{CC}z.long_range_mem{MEM}`, using similar notation as above (`{MEM}` refers to the ensemble member).

|         Description         |              Filename Pattern               |                                                        Example                                                        |
| --------------------------- | ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Point-type Channel Routing  | `{prefix}.channel_rt_{MEM}.f{FFF}.conus.nc` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/long_range_mem1/nwm.t00z.long_range.channel_rt_1.f006.conus.nc |
| 1km gridded Land Output     | `{prefix}.land_{MEM}.f{FFF}.conus.nc`       | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/long_range_mem1/nwm.t00z.long_range.land_1.f024.conus.nc       |
| Point-type Reservoir Output | `{prefix}.reservoir_{MEM}.f{FFF}.conus.nc`  | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/long_range_mem1/nwm.t00z.long_range.reservoir_1.f001.conus.nc  |

Long-range forecast data are only available for the Continental United States.

### USGS Observations

**USGS Timeslices**  15-minute observation data for the Continental United States. Each file begins with the prefix `nwm.{YYYYMMDD}/usgs_timeslices`, using similar notation as above.

|      Description      |                       Filename Pattern                        |                                                         Example                                                         |
| --------------------- | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| 15-minute observation | `{prefix}/{YYYY}-{MM}-{DD}_HH:mm:ss.15min.usgsTimeSlice.ncdf` | https://noaanwm.blob.core.windows.net/nwm/nwm.20230123/usgs_timeslices/2023-01-23_00%3A00%3A00.15min.usgsTimeSlice.ncdf |


where

* `HH` is the two-digit hour of the day
* `mm` is the two-digit minute of the hour
* `ss` is the two-digit second of the minute

USGS Timeslices data are only available for the Continental United States.

## Example

This example shows loading a short-range forecast for the Continental United States and plotting the soil saturation.

```python
>>> import adlfs
>>> import xarray as xr
>>> fs = adlfs.AzureBlobFileSystem("noaanwm")
>>> prefix = "nwm/nwm.20230123"
>>> ds = xr.open_dataset(fs.open(f"{prefix}/short_range/nwm.t00z.short_range.land.f001.conus.nc"))
>>> soil_saturation = ds["SOILSAT_TOP"].load()
>>> soil_saturation.coarsen(x=4, y=4, boundary="trim").mean().plot(figsize=(16, 10))
```

Which produces the figure

![soil saturation plot](https://ai4edatasetspublicassets.blob.core.windows.net/assets/notebook-output/noaa-nwm-soil-saturation.png)


See the [example notebook](https://nbviewer.jupyter.org/github/microsoft/AIforEarthDataSets/blob/main/data/noaa-nwm-example.ipynb) for more.