# Google Storage Bucket Inventory

#### census-database

This is where the bulk of the State Demography Office census data is backed up.  It is in the 'Nearline' storage class, which Google classifies as 'data that you do not expect to access frequently'.  If anything disastrous happens, data from these databases can be restored using pg\_restore (like so...):
```
pg_restore -h 104.196.8.243 -p 5433 -U postgres -j 2 -d dola /tmp/dola.custom
```

#### co-publicdata

Data is regularly dumped here by the ```nodecron``` container based on the ```codemog/co_cron``` image.  Special District gis files are dumped using ```pgsql2shp```, as well as BLS data files from the weekly polling of their API.  
This is also the default place to store any GIS file referenced by the [GIS Data Page](https://demography.dola.colorado.gov/gis/gis-data.html).
Any new file placed here is automatically set to be publicly available.

#### dola-db-dump

This is a repository for dumps of the ```dola``` database from the ```fastpostgres``` instance.  The other databases are relatively static and don't need to be backed up regularly.  These dumps are created weekly and timestamped by the ```nodecron``` container based on the ```codemog/co_cron``` image.  
Any new file placed here is automatically set to be publicly available.

#### maps-static

This bucket holds maps (PDF's, JPEG's or PNG's) that will be available as downloads throughout the site.  I could alternately have used Google Drive, but it's nice to have the maps available in a one clean container that I can look after.  
Any new file placed here is automatically set to be publicly available.