### Instructions

You'll save yourself a lot of trouble if you preload your security key during the Instance Creation Step.

##### Get your security key in place
Use Puttygen to create a key.  For everything you could possibly need, see link below:
 - https://gist.github.com/feczo/7282a6e00181fde4281b

##### Create instance on the Google Cloud Platform
These instructions are specific to CoreOS, a minimal Linux installation specifically suited to serving docker containers.  Do not use a different flavor of linux unless you know what you're doing.

![GCP Setup Image1](/img/setup1a.jpg)

Create a Slow (Magnetic 360GB) and a Fast (SSD 120GB) Disk

![GCP Setup Image2](/img/setup2a.jpg)

Enter your key here:

![GCP Setup Image3](/img/setup3.jpg)

##### Reserve Static IP
Add a pre-existing Static IP address here - or create a new one:

![GCP Setup Image4](/img/setup4.jpg)

##### Networking Rules
We're running two database containers, so we need to allow ports 5432 and 5433.  Our NodeJS microservices are running on ports 4001, 4002, and 4003.  Specific additional rules may apply based on which specific applications you want to serve.  After testing, lock down your database (and SSH) access by identifying and restricting service to local IPs.  

![GCP Setup Image5](/img/setup5.jpg)

#### SSH Instructions
Use PUTTY to login.

Start by formatting your drives. (Use the lsblk command to identify which drive is which. THEY MAY NOT BE /dev/sdb & /dev/sdc !):


Format Persistent Disks
```
sudo mkfs.ext4 /dev/sdb
sudo mkfs.ext4 /dev/sdc
```

Mount Magnetic Drive and Create a data directory for Postgres
```
cd /
sudo mkdir slow
sudo mount /dev/sdb /slow/

cd /slow
sudo mkdir pgdata
```

Mount SSD Drive and Create a data directory for Postgres
```
cd /
sudo mkdir fast
sudo mount /dev/sdc /fast/

cd /fast
sudo mkdir pgdata
```

CREATE DATA CONTAINERS
```
sudo docker create -v /slow/pgdata:/var/lib/postgresql/data --name slowdata busybox
sudo docker create -v /fast/pgdata:/var/lib/postgresql/data --name fastdata busybox
```

CREATE POSTGRES / POSTGIS CONTAINERS
```
sudo docker run --name slowpostgres -p 5432:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from slowdata mdillon/postgis:9.4
sudo docker run --name fastpostgres -p 5433:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from fastdata mdillon/postgis:9.4
```


Most everything is set up now.  You can log in to an FTP client like Filezilla (don't forget to load your key).  And you can also log in to PgAdmin (the credentials for both database clusters are the same with the exception of the port numbers; 5432 for magnetic, 5433 for ssd).

Before loading data, you will need to log in to BOTH containers via PgAdmin, and do the following steps for each:

 - Create the relevant databases for each cluster (dola, acs0812, acs0913, etc).
 - Add the postgis extension to each individual database.
 - Create a 'codemog' user, and set the codemog password in the SQL window as follows:

```
CREATE ROLE codemog;
ALTER USER codemog WITH PASSWORD 'whatever';
ALTER ROLE codemog LOGIN;
```
(The codemog user is a SELECT-only level user.)

### Now you are ready to upload data from the databases.

The data is stored in a google storage bucket called census-database.  Since CoreOS Linux does not contain pg\_restore and pg\_admin (it comes packaged with PgAdmin), you could:
 - install pgadmin3 on coreos (eh)
 - create a temporary postgis docker container from which to run these commands
 - use an intermediate cloud machine
 - use the (windows equivalent) commands on desktop

#### Don't type this:
Note, The .custom files were created with pg\_dump using a command such as the one below:
```
# pg_dump -Fc -h 104.197.26.248 -U postgres -p 5432 -d dola > dola.custom
```

#### Type this:
Use pg\_restore to restore database from a pg\_dump created file
```
pg_restore -h 104.196.8.243 -p 5433 -U postgres -j 2 -d dola /tmp/dola.custom
```
Remember to use the correct port depending on which database cluster you would like to use.
