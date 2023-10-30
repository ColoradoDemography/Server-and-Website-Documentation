# Troubleshooting the Website Server

## Try this first

If the front page stats are not populating, the coreas server is probably down. First stop and then start the dlg-coreos VM from the VM instances page in Google Cloud. Then SSH into the VM. It can usually be brought back up quickly with these commands

```
docker ps -a
(give it a few minutes, if the stats on the front of the website still don't show up, continue below)
docker restart postgres2
sudo -i
mount /dev/sdb /giant/
docker restart postgres2

```
Give it a few minutes for postgres to get going again. May have to try the restart and mount a couple times.

## Archival, reference only

If the website is down, the very first thing to check is the docker containers on the website server. There is an issue where every so often the containers break.

To check and fix this in one fell swoop, ssh into the `demography-website` instance on Google Cloud.  Then, run `docker ps -a` to simultaneously check for containers and reload them.

This should show you container status' of less then a second or so of uptime.  This should have fixed it.  If not, remove and reload the website containers using the steps below.

```
docker stop website demogproxy
docker rm website demogproxy

docker run --restart unless-stopped --name website -d -p 4008:4008 codemog/jekyll-website-build
docker run --restart unless-stopped  --name demogproxy -v /etc/letsencrypt/archive/demography.dola.colorado.gov:/ssl/docker --link website:website -p 443:443 -p 80:80 -d codemog/demog-proxy

```

If you need to rebuild the instance, you can, but before doing that check that the SSL certificates are up to date by running the code below:

```
docker stop website demogproxy
docker rm website demogproxy

docker run -it --rm -p 443:443 -p 80:80 --name certbot -v "/etc/letsencrypt:/etc/letsencrypt" -v "/var/lib/letsencrypt:/var/lib/letsencrypt" quay.io/letsencrypt/letsencrypt:latest renew

docker run --restart unless-stopped --name website -d -p 4008:4008 codemog/jekyll-website-build
docker run --restart unless-stopped  --name demogproxy -v /etc/letsencrypt/archive/demography.dola.colorado.gov:/ssl/docker --link website:website -p 443:443 -p 80:80 -d codemog/demog-proxy

```

That should check the SSL certificates for renewal, then renew them if needed.  If you do end up renewing them, you'll need to update the index.js file in the demogproxy container.
To do this, you'll need to go to the file on [Github](https://github.com/ColoradoDemography/demog-proxy/blob/master/index.js) and make sure you add one digit to the file names for the sslobj on lines 38,39, and 40.
Commit these changes, then log into Docker Hub and wait for the container to rebuild (look at the Build Details tab). 
Then run these commands:

``` 
docker stop website demogproxy
docker rm demogproxy website

docker pull codemog/demog-proxy

docker run --restart unless-stopped --name website -d -p 4008:4008 codemog/jekyll-website-build
docker run --restart unless-stopped  --name demogproxy -v /etc/letsencrypt/archive/demography.dola.colorado.gov:/ssl/docker --link website:website -p 443:443 -p 80:80 -d codemog/demog-proxy

```

If you really want to rebuild the instance, use a g1-small instance with a 15g boot disk.  Make sure to allocate the default network settings.

Then, run these docker commands:

```
docker run --restart unless-stopped --name website -d -p 4008:4008 codemog/jekyll-website-build
docker run --restart unless-stopped  --name demogproxy -v /etc/letsencrypt/archive/demography.dola.colorado.gov:/ssl/docker --link website:website -p 443:443 -p 80:80 -d codemog/demog-proxy

```

