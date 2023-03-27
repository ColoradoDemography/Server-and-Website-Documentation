## Postgres Database Restore

If you're reading this...I'm sorry.  This guide will help you get the databases back up.
Take a breath, you'll be fine.

### What to check

If things are down, specifically the databases and nothing else, run through these steps.

1. Container Status
2. Disk Status
3. Data Presence

After you figure out where the failure is 
#### Rebuild the Containers

Typically, if the databases are down, the containers are down.  To check this, log into
the `dlg-coreos` instance and run the command `docker ps -a`.  This will show the status of all containers.
If the fastpostgres and/or slowpostgres are exited, then they are down.  

You'll also want to check the fast and slow containers are created still.  They are built on busybox
images.  These help map where our data lives on the disks to the database containers. 

If these are down, you'll need to rebuild them.  Use the following commands:

CREATE DATA CONTAINERS (If needed)
```
docker create -v /slow/pgdata:/var/lib/postgresql/data --name slowdata busybox
docker create -v /fast/pgdata:/var/lib/postgresql/data --name fastdata busybox
```

CREATE POSTGRES / POSTGIS CONTAINERS

Changing the password here is helpful.  You will need to create the 'codemog' user and add permissions manually.  Check in PG Admin
```
docker run --name slowpostgres -p 5432:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from slowdata mdillon/postgis:9.4
docker run --name fastpostgres -p 5433:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from fastdata mdillon/postgis:9.4
```

#### Disk Status

It's unlikely, but possible that the disks `fast-coreos` and `slow-coreos` are up and running.  
You can check that by logging into the Google Cloud Console, clicking on 'Compute Engine' under the 
'Resources' box, then clicking on the 'Disks' link in the left hand column.  There should be green checks there.

#### Data Presence

There should be a lot of data, very big files, in the `/fast/pgdata/` and `/slow/pgdata/` folders.  
If there isn't, then the data is gone and you'll need to restore them using backups we make into our Google Storage buckets.

### Restoring the data 

This is really time consuming, but really not that hard.

Here is the basic overview:

1. Download most recent back-ups from Google Storage to another instance or a local machine.
2. Restore the data using `pg_restore`.
3. Add a codemog user and adjust permissions.


Three easy steps.

Make sure you do the DOLA data first, people can't get that anywhere else.

#### Download most recent Back-ups

Our data are backed up to Google Storage.  The Census data that doesn't change is only backed up once.
The DOLA data, that changes more often is backed-up every week and the files get time stamped.

To download the data, log into the Google Cloud Console, clicking on 'Storage' under the 
'Resources' box.  The DOLA data is in the aptly named `dola-db-dump` bucket and the Census data is in the
`census-database` bucket.

Make sure to monitor storage on whatever machine your using, local or additional instance.

Download the most recent `dola.custom` file using the time stamps on the files.  

Download the backups for each census dataset one at a time.

#### Upload the data using PG_Restore

Now we need to repopulate the database with those dumps.

I recommend using a local computer because the utility `pg_restore` is bundled with PGAdmin, 
not postgres itself.  This means that you could load PGAdmin on a server, but you likely already have it 
locally.

First, create a blank database to dump the file into. The database name needs to be the EXACT same as it was, so DOLA data gets put into the dola database.  The .custom file
has that information in the filename for you.

Second, you'll need to start the restore. To run this on Windows, use the following command:

```
pg_restore -h gis.dola.colorado.gov -p PORT -U postgres -j 2 -d DBBEINGRESTORED PATHTO.customFILE

```

You'll need to update the port to 5433 if you're using the fastpostgres DB and 5432 if you're using slowpostgres.
Change `DBBEINGRESTORED` to the name of the database being restored and `PATHTO.customFILE` to the file path to the 
.custom file.

#### Permissions

After you load each database, you'll need to add the `codemog` role to the database using PGAdmin.
Then you'll need to add access to the schema and then making sure that select permissions are added to each table.

To add codemog to the Schema and tables open up a SQL window in PGAdmin then use this command, substituting the relevant schema.

```
GRANT USAGE ON SCHEMA schema TO codemog;
GRANT SELECT ON ALL TABLES IN SCHEMA schema TO codemog;

```
