# Docker Container Inventory

**All Containers are on DockerHub, account: codemog**

Run ```docker pull codemog/imagename``` to get the latest version of a container.


##gis.dola.colorado.gov

portainer/portainer
```
docker run --restart unless-stopped --name portainer -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer
```

codemog/ms\_demog\_lookups
```
docker run --restart unless-stopped --name demoglookup -d -p 4001:4001 codemog/ms_demog_lookups
```

codemog/ms\_censusapi
```
docker run --restart unless-stopped --name censusapi -d -p 4002:4002 codemog/ms_censusapi
```

codemog/ms\_censusmap
```
docker run --restart unless-stopped --name censusmap -d -p 4003:4003 codemog/ms_censusmap
```

codemog/co-fs-grants
```
docker run --restart unless-stopped --name cogrants -d -p 4004:4004 codemog/co-fs-grants
```

codemog/codemog-shiny-server
```
docker run --restart unless-stopped --name shiny-server -d -p 3838:3838 codemog/shinydockerfile
```

codemog/point2placeapi
```
docker run --restart unless-stopped --name pt2pl -d -p 4005:4005 codemog/point2placeapi
```

codemog/special\_districts\_api
```
docker run --restart unless-stopped --name sdapi -d -p 4006:4006 codemog/special_districts_api
```

codemog/phantomprint
```
docker run --restart unless-stopped --name phantom -d -p 4007:4007 codemog/phantomprint
```

codemog/co\_cron
```
docker run --restart unless-stopped --name nodecron -d -v /gcp:/root codemog/co_cron
```

codemog/muni\_api
```
docker run --restart unless-stopped --name muniapi -d -p 4010:4010 codemog/muni_api
```

codemog/node-proxy - If not using State SSL, set up using Let's Encrypt and mirror demog-proxy file and folder mapping
```
docker run --restart unless-stopped  --name nodeproxy -v /etc/letsencrypt/archive/gis.dola.colorado.gov:/ssl/docker --link demoglookup:demoglookup --link shiny-server:shiny-server --link censusmap:censusmap --link censusapi:censusapi --link muniapi:muniapi --link phantom:phantom --link cogrants:cogrants --link sdapi:sdapi --link pt2pl:pt2pl -p 443:443 -p 80:80 -d codemog/node-proxy
```
*use the <b>--link name</b> command to link by name all your application and microservice containers (the ones with port mapping - excluding the databases) to the proxy*




##demography.dola.colorado.gov

codemog/jekyll-website-build
```
docker run --restart unless-stopped --name website -d -p 4008:4008 codemog/jekyll-website-build
```

codemog/demog-proxy
```
docker run --restart unless-stopped  --name demogproxy -v /etc/letsencrypt/archive/demography.dola.colorado.gov:/ssl/docker --link website:website --link shiny-server:shiny-server -p 443:443 -p 80:80 -d codemog/demog-proxy
```



Optional (for logging):

- --log-opt max-size=[0-9+][k|m|g]
- --log-opt max-file=[0-9+]



### Database & Data Volume Containers
(gis.dola.colorado.gov)


*Do these in order, and note the password parameter*

**Data Containers**
```
docker create -v /giant/pgdata:/var/lib/postgresql/data --name slowdata busybox
```

**Postgres/PostGIS Containers** Just letters/numbers for password, no " or '
```
docker run --restart unless-stopped --name postgres -p 5433:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from slowdata mdillon/postgis:9.4
```
When pulling new postgres, it may be necessary to install or upgrade postgis in the geography databases
