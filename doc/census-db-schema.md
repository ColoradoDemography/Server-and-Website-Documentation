# CensusAPI_DB

## About the Colorado State Demography Office's Census Databases

**About**: This is a PostgreSQL/PostGIS Database Cluster with information at the State, County, Place, Tract, and Block Group Levels of Geography (and more) for the entire United States.  Currently, it includes data from the 1980, 1990, 2000 and 2010 Census, as well as the 2008-2012 5Y, and 2009-2013 5Y American Community Surveys.


The construction of each of the Census Databases was done with performance in mind.  It is designed specifically for mapping applications, where retrieving large volumes of spatial data quickly is a necessity.


Each Census Dataset is located in a separate database in the cluster.  Currently available are the 1980 Census (sf1 &amp; sf3), 1990 Census (sf1 &amp; sf3), 2000 Census (sf1 &amp; sf3), 2010 Census, 2008-2012 ACS, 2009-2013 ACS.


Because speed and data storage costs were a major concern, the data has been paired down to only the most common geography levels.

**1980**: State, County, Place, Tract, Block Group  (for 1980, Tract and Block Group data is not available nationwide)

**1990**: State, County, Place, Tract, Block Group

**2000**: State, County, Place, Tract, Block Group

**2010**: State, County, Place, Tract, Block Group, ZCTA, SDUNI, SDELM, SDSEC, COUSUB

**ACS 08-12**: State, County, Place, Tract, Block Group, ZCTA, SDUNI, SDELM, SDSEC, COUSUB

**ACS 09-13**: State, County, Place, Tract, Block Group, ZCTA, SDUNI, SDELM, SDSEC, COUSUB

**ACS 10-14**: State, County, Place, Tract, Block Group, ZCTA, SDUNI, SDELM, SDSEC, COUSUB


Geography sources available for each dataset:
<p><b>1980</b>: <a href="https://www.nhgis.org/" target="_blank" >NHGIS</a> (State, County, Place, Tract - no Block Group)
<p><b>1990</b>: <a href="https://www.nhgis.org/" target="_blank" >NHGIS</a>, <a href="https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html" target="_blank">Tiger Cartographic Boundaries</a>
<p><b>2000</b>: <a href="https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html" target="_blank">Tiger Cartographic Boundaries</a>, <a href="https://www.census.gov/geo/maps-data/data/tiger-line.html" target="_blank">Tiger Shapefiles</a></p>
<p><b>2010</b>: <a href="https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html" target="_blank">Tiger Cartographic Boundaries</a>, <a href="https://www.census.gov/geo/maps-data/data/tiger-line.html" target="_blank">Tiger Shapefiles</a></p>
<p><b>ACS 08-12</b>: <a href="https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html" target="_blank">Tiger Cartographic Boundaries</a>, <a href="https://www.census.gov/geo/maps-data/data/tiger-line.html" target="_blank">Tiger Shapefiles</a></p>
<p><b>ACS 09-13</b>: <a href="https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html" target="_blank">Tiger Cartographic Boundaries</a>, <a href="https://www.census.gov/geo/maps-data/data/tiger-line.html" target="_blank">Tiger Shapefiles</a></p>

<h3>Database Structure</h3>
<p>Each database centers on the concept of a <i>geonum</i>.  A geonum is much like the census 'geoid' (or FIPS code), except, the geonum is an integer value that never begins with a leading '0'.  For instance, the census geoid for Denver County, Colorado would be the string '08031', while in our databases, the unique geonum would be the integer 108031.  For the basic geographies, the geonum is essentially the same as the geoid, but with a preceeding '1'.</p>

<p>Each database is divided into schemas.  Typically, there will be geographic schemas ('nhgis', 'carto', 'tiger'), table schemas ('sf1', 'sf3', or 'data') where the census data resides, and a search schema ('search').</p>

<p>Data can be retrieved from individual tables by joining from either geography, or from the search schema tables.</p>
<p>Example to select all tracts in Denver County, Colorado including Housing Units information (h1) using the search schema (c2010): </p>

<p><i>SELECT * FROM search.data NATURAL JOIN data.h1 WHERE state=8 AND county=31 AND sumlev=140;</i></p>

<p>Example to select all places in California, including Housing Units information (h1) using carto geography schema (c2010): </p>
<p><i>SELECT * FROM carto.place NATURAL JOIN data.h1 WHERE state=6;</i></p>


<h2>Instructions on How to Set Up Your Own Instance</h2>

<p>You are free to use the main instance for small tasks and minor applications. (Expect there will be occasional downtime!)  </p>
<p>We (The Colorado State Demography Office) are currently running on an Amazon T2 Micro Instance, so we do not have a lot of spare capacity.  If you intend to create a major application with significant bandwidth demands, we would like it if you set up your own instance.</p>  <p>While copying our Database and API is free of charge (and encouraged), you will still incur fees from Amazon for hosting your own instance.<p>
<p><b>Instructions:</b></p>
<p>Quick Setup : From Amazon Machine Image</p>
<p>Make Sure Your Region is Located in US West: Oregon.  Then, Launch a New Instance</p><br /><br />
<img src="image/launch.jpg" />
<br /><br />
<img src="image/choose_ami.jpg" />
<br /><br />
<p>Select 'Community AMIs in the left menu.  Search for ami-a997b699.  Then Select.</p>
<p>Under 'Choose an Instance Type':  Choose an instance appropriate to your workload.  (I would recommend an EBS only instance).  We currently run ours on a T2 micro instance with no issues.  Choose 'Next: Configure Instance Details' to move on to the next screen</p>
<p>Under 'Configure Instance Details': accept the defaults.  Then press 'Next: Add Storage' to move on to the next screen.</p><br />
<img src="image/addstorage.jpg" /><br /><br />
<p>Under 'Add Storage'.  Click 'Add New Volume'.  See image above.  The Device should be /dev/sdf, the snapshot should be snap-dc0d195d, the size should be 280GB, and I would advise you to choose 'Delete on Termination' to avoid potentially racking up a bill for storage if you decide to terminate your instance.  Choose 'Next: Tag Instance'.</p>
<p>Under 'Tag Instance', you can choose to move on without entering anything here.  Click 'Next: Configure Security Group'.</p>
<p>Under 'Configure Security Group', you can choose to move on without entering anything here.  Important: See section below to configure the security group AFTER the instance is set up.  This is important, as nothing will work under the default conditions.  Click 'Review and Launch', then 'Launch' again at the next screen.  You will be asked to set up a security key if you have not done so before.  Please consult the <a href="http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html" target="_blank">Amazon Help</a> if you have not gone through this process before.</p><br />
<img src="image/ready.jpg" /><br /><br />
<p>When your instance is finished setting up, it will look like the above photo. The first thing you'll want to do is change the security group settings.  First, take note of your public IP address.  You'll need it in a second.</p>
<p>In the Security Group Area, you'll probably want to add a few rules.  I recommend the following:</p>
<p>Port 5432 (Postgres), Allow access for the Instance Public IP Address.</p>
<p>Port 5432 (Postgres), Allow access for your personal computer IP Address (This will allow you to use programs like PG Admin).</p>
<p>Port 22, Allow access to your personal computer IP Address (This will allow you to use SSH or FTP to access your instance).</p>
<p>Port 80, Allow access to everyone (0.0.0.0/0) Internet HTTP Access.</p>
<p>Port 443, Allow access to everyone (0.0.0.0/0) Internet HTTPS Access.</p>
<p>Importantly, if you plan on adding sensitive information to your server, you may want to consider re-visting these settings, as well as modifying your pg_hba.conf and postgresql.conf files for tighter security.</p><br />
<img src="image/ssh.jpg" /><br /><br />
<p>The last step is the most difficult.  You need to connect to your server through SSH.  You can use putty if you are familiar with it.  Otherwise, select your instance in the AWS console and press 'Connect'.  Choose 'A Java SSH Client directly from my browser (Java required)'.  Make sure the username is set to 'ubuntu', and that the proper security key is chosen.</p>
<p>In the console, enter the following commands:</p>
<p>First you'll need to attach the data volume to your instance</p>
```
sudo mount /dev/xvdf /mnt
```
<p>Next, you'll want to restart the PostgreSQL server</p>
```
sudo /etc/init.d/postgresql restart
```
<p>Then you'll need to login as the postgres user and set the proper passwords.  First, set the password for the 'codemog' user to 'demography'.  This is a SELECT only level user.  The password must be set to 'demography' in order to work out-of-the-box with the pre-installed GitHub repositories for the Census API and Census Map.</p>
<p>To login as the postgres user:</p>
```
sudo su postgres
```
<p>To open the psql program:</p>
```
psql
```
<p>To change the codemog user password</p>
```
ALTER USER codemog WITH PASSWORD 'demography';
```
<p>Now change the main postgres user password.  This can be whatever you would like it to be, just don't forget it!</p>
```
ALTER USER postgres WITH PASSWORD 'password';
```
<p>To exit psql:</p>
```
\q
```
<p>You can close the console now.</p>
<p>To test your instance, enter your public IP address into the address bar of your web browser, followed by:</p>
```
/CensusAPI_Map/index.html
```
<p>If successfull, you will see the Census Data Map!</p>



