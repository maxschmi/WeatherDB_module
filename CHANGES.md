# Change-log

## Version 0.0.14
- added type test, if parameter gets checked for "all"
- specify that secrets_weatherDB file should be on PYTHONPATH environment variable
- Changed DGM5 to Copernicus DGM25, because of license advantages
- adjusted update_horizon methode to be able to work with different CRS
- add kwargs to update_richter_class of StationsN
- fix get_geom with crs transforamation

## Version 0.0.13
- change the timezone allocation method of the precipitation download df
- set freq to 10 minutes of precipitation download, to be able to overwrite Values with NAs
- add remove_nas parameter to overwrite new NAs in the database. (mainly for programming changes)
- define the name of the geometry column in get_meta.

## Version 0.0.12
- add quality check for precipitation stations: delete values were the aggregated daily sum is more than double of the daily measurement
- when filling up also replace the filled_by column if it got changed
- TimestampPeriod class now also detects string inputs as date
- major error fixed: the coefficients calculation in the fillup method was the wrong way around
- for daily parameters the expand_timeseries_to_period ads now 23:50 to max_tstp_last_imp to get the period
- add vacuum cleanup method in Broker
- check precipitation df_raw for values below 0
- add stids parameter to last_imp methods of stations classes
- add an update method to stations classes, to do a complete update of the stations database data (update_raw + quality_check + fillup + richter_correct)
- only set start_tstp_last_imp values in db if update_raw is done for all the stations
  
## Version 0.0.11
- add fallback on thread if multiprocessing is not working
- cleaning up ftplib use. allways recreate a new instance and don't try to reuse the instance.
  This resolves some problems with the threading of the instances.
- clean raw updates of only recent files by the maximum timestamp of the historical data.

## Version 0.0.10
- fixed get_adj compare Timestamp with timezone 

## Version 0.0.9
- fixed future warning in stations.GroupStations().create_ts
- stations.GroupStations().create_roger_ts fixed
- removed join_how from _check_period as it was not used
- fixed StationND().get_adj, because the StationNBase.get_adj was only for 10 minute resolution
- get_adj always based on "filled" data
  
## Version 0.0.8
- fixed installation (psycopg2 problem and DB_ENG creation)
- fixed importing module when not super user

## Version 0.0.7
- convert timezone of downloaded precipitation data, because (before 200 the data is in "MEZ" afterwards in "UTC")
- update_ma: 
  - Rasters now also have proj4 code, if necessary. Because the postgis database is not supporting transformation to EPSG:31467 
  - small speed improvement
- StationCanVirtual._check_meta updated to check separately if station is in meta table and if it has a timeseries table
- Added timezone support. The database timezone is UTC.

## Version 0.0.6
- error fixed with is_virtual (!important error!)
- human readable format for the period in log message added
- some spelling errors fixed in documentation
- kwargs added to child methods of get_df (like get_raw...)
- in get_df and consecutive methods: 
  - filled_share column added if aggregating and filled_by selected
  - possibility to download filled_by added
  - nas_allowed option added
  - add_na_share option added. (give the share of NAs if aggregating) 
- in create_ts option to save several kinds added
- get_max_period method
- error in check_stids fixed
- error in ma_update fixed

## Version 0.0.5
- The et_et0 parameter gor renamed to r_r0 in the create_ts method
- The r_r0 is now possible to add as pd.Serie or list, when creating a timeserie file
- get_meta method of single stations updated
- get_meta for GroupStation(s) updated
- get_df for GroupStation added
- Quickstart added to the documentation
- documentation has now a TOC tree per class and a method TOC tree on top
- option to skip the check if a station is in the meta file, this is used for computational advantages in the stations classes, because they test already before creating the objects if they are in the meta table.
- ..._von and ..._bis columns got renamed to the english name ..._from and ..._until
- the quot_... fields got all normed to % as unit
- dropping stations from meta while updating checks now if stid is in downloaded meta file

## Version 0.0.4
- The method part was added to the documentation 
- the connection method got updated

## Version 0.0.3
This is the first released version