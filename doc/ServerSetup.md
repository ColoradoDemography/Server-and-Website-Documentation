### Instructions

You'll save yourself a lot of trouble if you preload your security key during the Instance Creation Step.

##### Get your security key in place
Use Puttygen to create a key.  For everything you could possibly need, see link below:
 - https://gist.github.com/feczo/7282a6e00181fde4281b

##### Create instance on the Google Cloud Platform
These instructions are specific to Ubuntu 14.04.  Do not use a different flavor of linux unless you know what you're doing.

![GCP Setup Image1](/img/setup1.jpg)

Create a Magnetic (400GB) and a SSD (120GB) Drive

![GCP Setup Image2](/img/setup2.jpg)

Enter your key here:

![GCP Setup Image3](/img/setup3.jpg)

##### Reserve Static IP
Add a pre-existing Static IP address here - or create a new one:

![GCP Setup Image4](/img/setup4.jpg)

##### Networking Rules
We're running two database clusters, so we need to allow ports 5432 and 5433.  Later, lock down your database (and SSH) access by identifying and restricting service to local IPs.  (Also see security settings in pg\_hba and postgresql.conf files).  

![GCP Setup Image5](/img/setup5.jpg)

#### SSH Instructions
Use PUTTY to login.

Start by formatting your 400GB magnetic drive. (Use the lsblk command to identify which drive is which. YOUR MAGNETIC DRIVE MAYBE NOT BE /dev/sdb !):
```
sudo mkfs.ext4 /dev/sdb
```
Then create a new directory (we're calling ours 'dr') and mount your drive there:
```
cd /
sudo mkdir dr
sudo mount /dev/sdb /dr/
```
##### Info about Postgis Install:  
 - http://trac.osgeo.org/postgis/wiki/UsersWikiPostGIS21UbuntuPGSQL93Apt
 
The versions of PostgreSQL/PostGIS we need may not be available with the APT-GET command by default.  Add them with the following commands:
```
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt trusty-pgdg main" >> /etc/apt/sources.list'
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
```
Then install:
```
sudo apt-get install postgresql-9.4-postgis-2.1 pgadmin3 postgresql-contrib-9.4
```
We're going to be very specific about where we want our data to go.  We'll delete the default database cluster:
```
sudo pg_dropcluster 9.4 main --stop
```
Then we'll create a new directory on our mounted drive in which to store the data:
```
cd /dr
sudo mkdir pgdata
```
And we'll assign permissions for our postgres user (who was auto-created during the installation of PostgreSQL):
```
sudo chown -R postgres:postgres /dr/pgdata
sudo chmod 700 /dr/pgdata
```
Now we'll initialize our new cluster there:
```
sudo pg_createcluster -d /dr/pgdata/data -l /dr/pgdata/log --start-conf auto 9.4 main
```
##### Edit the following two files per the below instructions:  
 - See https://cloud.google.com/solutions/setup-postgres
```
sudo vi /etc/postgresql/9.4/main/postgresql.conf
sudo vi /etc/postgresql/9.4/main/pg_hba.conf
```
Now restart PostgreSQL
```
sudo service postgresql restart
```
Now we'll want to be able to use PgAdmin using standard password access.  We'll need to assign a password to the postgres user:
```
sudo su -
su postgres
psql
```
In PSQL:
```
\password **whatever**
\q
```
Now exit out of postgres and root users and back to our default user.
```
exit
exit
```

##### Install git, apache, nodejs, npm, php, php-postgres driver
```
sudo apt-get install git
sudo apt-get install apache2
sudo apt-get install nodejs
sudo apt-get install npm
sudo apt-get install php5
sudo apt-get install php5-pgsql
```
##### Restart Apache
```
sudo service apache2 restart
```
##### Map nodejs command to node
```
sudo ln -s /usr/bin/nodejs /usr/bin/node
```
##### Git Clone Repos in Apache Webserver Directory
```
cd /var/www/html
git clone https://github.com/royhobbstn/CensusAPI.git
```
##### Add New PostgreSQL Cluster on a SSD drive
The ACS Webmap needs much more speed than the other applications.  To balance cost with performance, we create an additional PostgreSQL cluster on a SSD hard drive.


##### create temp directory under /dr/
##### change permissions of temp to everyone 
sudo chmod 777 temp
#####use ftp to upload .custom files to temp


##### Use SSH to createuser at commandline:  
 - codemog is SELECT only access user
 - postgresql users are really just linux users
```
createuser codemog
```
##### use pgadmin SQL window to change user codemog password
```
ALTER USER codemog WITH PASSWORD 'whatever';
```
## Use pg_restore command to restore database from a pg_dump created file
```
pg_restore -h 104.197.26.248 -p 5432 -U postgres -j 2 -d acs1014 /dr/temp/acs1014.custom
```