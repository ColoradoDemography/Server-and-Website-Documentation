## Instructions

You'll save yourself a lot of trouble if you preload your security key during the Instance Creation Step.

## Get your security key in place
Use Puttygen to create a key.  For everything you could possibly need, see link below:
https://gist.github.com/feczo/7282a6e00181fde4281b

## Create instance on the Google Cloud Platform
Ubuntu 14.04 "trusty"

## Reserve Static IP

## Networking Rules


#SSH Instructions

cd /
lsblk
sudo mkfs.ext4 /dev/sdb
sudo mkdir dr
sudo mount /dev/sdb /dr/
cd dr
sudo mkdir pgdata

###info about postgis install:  http://trac.osgeo.org/postgis/wiki/UsersWikiPostGIS21UbuntuPGSQL93Apt

sudo lsb_release -a 
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt trusty-pgdg main" >> /etc/apt/sources.list'
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql-9.4-postgis-2.1 pgadmin3 postgresql-contrib-9.4
sudo pg_dropcluster 9.4 main --stop

sudo chown -R postgres:postgres /dr/pgdata
sudo chmod 700 /dr/pgdata


cd /
sudo pg_createcluster -d /dr/pgdata/data -l /dr/pgdata/log --start-conf auto 9.4 main


#See https://cloud.google.com/solutions/setup-postgres
---------------------
:set nocompatible
sudo vi /etc/postgresql/9.4/main/postgresql.conf
sudo vi /etc/postgresql/9.4/main/pg_hba.conf
---------------------

sudo service postgresql restart
sudo su -
su postgres
psql

\password *****
\q

exit #out of postgres
exit #out of root

#create temp directory under /dr/
#change permissions of temp to everyone 
sudo chmod 777 temp
##use ftp to upload .custom files to temp

##connect to pgadmin
##create database acs1014 (or dola)

##use SSH to createuser at commandline:  codemog is SELECT only access user
createuser codemog

##use pgadmin SQL window to change user codemog password
ALTER USER davide WITH PASSWORD 'hu8jmn3';

##restore database
pg_restore -h 104.197.26.248 -p 5432 -U postgres -j 2 -d acs1014 /dr/temp/acs1014.custom


##install git
sudo apt-get install git
##install apache
sudo apt-get install apache2
##install php
sudo apt-get install php5

##install postgresql driver php
sudo apt-get install php5-pgsql

##restart apache
sudo service apache2 restart

sudo apt-get install nodejs
sudo apt-get install npm
sudo ln -s /usr/bin/nodejs /usr/bin/node

##git clone repos


#add new cluster



## General Info

Instance
 - Ubuntu 14.04 "trusty"
Apache Webserver Directory:
 - /var/www/html/
