# Docker Container Inventory

**All Containers are on DockerHub, account: codemog**

Run ```docker pull codemog/imagename``` to get the latest version of a container.


#### Application & Microservice Containers

codemog/ms\_demog\_lookups
```
docker run --name demoglookup -d -p 4001:4001 codemog/ms_demog_lookups
```

codemog/ms\_censusapi
```
docker run --name censusapi -d -p 4002:4002 codemog/ms_census_api
```

codemog/ms\_censusmap
```
docker run --name censusmap -d -p 4003:4003 codemog/ms_census_api
```

codemog/codemog-shiny-server
```
docker run --name shiny-server -d -p 3838:3838 codemog/codemog-shiny-server
```

codemog/co\_cron
```
docker run --name nodecron -d -v /gcp:/root codemog/co_cron
```


codemog/node-proxy
```
docker run --name nodeproxy --link demoglookup --link censusapi --link censusmap --link shiny-server -p 80:3000 -d codemog/node-proxy
```
*use the <b>--link name</b> command to link by name all your application and microservice containers (the ones with port mapping - excluding the databases) to the proxy*


#### Database & Data Volume Containers

*Do these in order, and note the password parameter*

**Data Containers**
```
sudo docker create -v /slow/pgdata:/var/lib/postgresql/data --name slowdata busybox
sudo docker create -v /fast/pgdata:/var/lib/postgresql/data --name fastdata busybox
```

**Postgres/PostGIS Containers**
```
sudo docker run --name slowpostgres -p 5432:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from slowdata mdillon/postgis:9.4
sudo docker run --name fastpostgres -p 5433:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from fastdata mdillon/postgis:9.4
```


