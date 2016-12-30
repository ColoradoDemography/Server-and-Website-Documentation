## What if the Whole Server Dies?

...or needs to be completely re-built.  This process proved to be somewhat distinct frombuilding the server from scratch
and deserved it's own documentation.

#### Relax

It's a bit scary to have the whole server down, but just breath and take it one step at a time.

### Outline of steps

1. Remove old instance.
2. Create a new instance identical to the old one.
3. Re-load all Docker containers.  
4. Generate and load SSL.

### Remove old insstance

Scary as this may be, you just need to go into the Google Cloud Platform: Compute Instance section,
highlight the instance that is being replaced, and then click delete.  The other steps won't work if you don't.

### Re-create instance

This section is nearly a direct rip-off of our [server set-up](https://github.com/ColoradoDemography/Server-and-Website-Documentation/blob/master/doc/server-setup.md),
but tweaked to be relevant to restoring a server.

##### If you use PUTTY or intend to ever load files to the server....

You'll save yourself a lot of trouble if you preload your security key during the Instance Creation Step.

Use Puttygen to create a key.  For everything you could possibly need, see link below:
 - https://gist.github.com/feczo/7282a6e00181fde4281b

##### Create instance on the Google Cloud Platform
These instructions are specific to CoreOS, a minimal Linux installation specifically suited to serving docker containers.

![GCP Setup Image1](/img/restore-2.png)

1. Name the new instance 'dlg-coreos'
2. Change the OD to CoreOS and set the Boot Disk to 40 GB as shown below.
3. Make sure to allow both types of traffic

![GCP Setup Image2](/img/restore-3.png)

Create a 'giant' 850 GB Persistent Disk, then edit dlg-coreos and add giant as an additional disk:

![GCP Setup Image3](/img/setup2a.jpg)

Enter your key here:

![GCP Setup Image3](/img/setup3.jpg)

##### Reserve Static IP
Add a pre-existing Static IP address: gis-server-address.

![GCP Setup Image4](/img/setup4.jpg)

##### Networking Rules
The current default network rules should cover this, but here is what they need to be.  It's good to check. We're running two database containers, so we need to allow ports 5432 and 5433.  Our NodeJS microservices are running on ports 4001, 4002, and 4003.  Specific additional rules may apply based on which specific applications you want to serve.  

![GCP Setup Image5](/img/setup5.jpg)

##### Don't forget to enable access to all Google Cloud APIs
This will come in handy.  Trust me.

![GCP Setup Image6](/img/setup6.jpg)

#### SSH Instructions
Use PUTTY to login OR do as Rob does and use the web based SSH through the GCP Dashboard.

Unless you have recreated giant from scratch, don't format your drives, they exist and have your data on them. **(Use the lsblk command to identify which drive is which. THEY MAY NOT BE /dev/sdb & /dev/sdc !)**.

Mount Magnetic Drive and Create a data directory for Postgres
```
cd /
mkdir giant
mount /dev/sdb /giant/

cd /giant
mkdir pgdata
```

```

Create Directory for Keys - (can be mounted into a docker container)
```
cd /
sudo mkdir gcp
```


Set up filezilla using your key and add the following keys to /gcp/:
- .pgpass for working with Postgres Databases (using pg_dump or pgsql2shp) - See Postgres documentation but follows this structure: ```hostname:port:database:username:password```
- Google Cloud Platform API Key (for uploading to Google Storage Buckets)
   - Menu: API Manager -> Credentials -> Create credentials (to aquire this key)
     - You need to do this each time. It is a .json file you download then you'll filezilla them in.

Load the Key Files using Filezilla

First, change the permissions for the gcp folder
```
sudo chmod 777 /gcp/
```
THIS IS A SUPER VULNERABLE PERMISSION SET, LOAD FILES THEN RUN THIS to restrict it:

```
sudo chmod 700 /gcp/
```

After loading the keyfiles, change the permissions:
```
sudo chmod 600 .pgpass
sudo chmod 600 whateverkeyfilename.json
```

#### Reload Docker containers


CREATE DATA CONTAINERS
```
docker create -v /giant/pgdata:/var/lib/postgresql/data --name slowdata busybox
```

CREATE POSTGRES / POSTGIS CONTAINERS

Changing the password here is helpful.  You will need to create the 'codemog' user I think.  Check in PG Admin
```
docker run --restart unless-stopped --name postgres -p 5433:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from slowdata mdillon/postgis:9.4
```


#### SSL Set-up

This section is inextricably linked to the node-proxy Docker Container, but the process needs to be run on the server first.



##### Generate new certificates

Free SSL is provided by [Let's Encrypt](https://letsencrypt.org/).  In the 'Spirit of Docker', all updates to SSL can be run through a temporary Docker container that is executed, then removed.  To update SSL, the nodeproxy container must not be started yet or stopped temoporarily.

1) Stop nodeproxy container if running (check with ```docker ps -a``` and look for a container with that name) using the ```docker stop nodeproxy```.

```
docker run -it --rm -p 443:443 -p 80:80 --name certbot -v "/etc/letsencrypt:/etc/letsencrypt" -v "/var/lib/letsencrypt:/var/lib/letsencrypt" quay.io/letsencrypt/letsencrypt:latest certonly

```
Choose standalone option, give it gis.dola.colorado.gov or a domain.
##### Connect the proxy to the certificates

1) Ensure that the digits in the sslobj variable in the index.js file of the node-proxy container are the same as the ones created by letsencrupt (i.e. cert1.pem).


2) Run these commands:

```
docker stop nodeproxy
docker rm nodeproxy
docker pull codemog/node-proxy 

docker run --restart unless-stopped  --name nodeproxy -v /etc/letsencrypt/archive/gis.dola.colorado.gov:/ssl/docker --link demoglookup:demoglookup --link shiny-server:shiny-server --link censusmap:censusmap --link censusapi:censusapi --link phantom:phantom --link cogrants:cogrants --link sdapi:sdapi --link pt2pl:pt2pl -p 443:443 -p 80:80 -d codemog/node-proxy

```
This provides a link between the pem files stored in /etc/letsencrypt/archive/gis.dola.colorado.gov and /ssl/docker, where the variables in the nodeproxy index.js file point.

__USE THIS SITE IF YOU NEED A NEW CERTIFICATE__

Adapted from: http://letsencrypt.readthedocs.io/en/latest/using.html#running-with-docker

&

https://certbot.eff.org/docs/using.html#renewal

Most everything is set up now.  And you can also log in to PgAdmin (the credentials for both database clusters are the same with the exception of the port numbers; 5432 for magnetic, 5433 for ssd).
