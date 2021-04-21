## SSL Certificates seem important.  Do I need to renew them?

SSL Certificates are really important. They allow us to securely connect to our clients using https.  Generally, if you're asking you need to renew them.  Plus, running the renewal process will stop you if you don't, but probably you need to.

## But first, dockerhub.com

I know this sounds weird, but you actually need to prep the last step before you start.  Actually, that sounds pretty normal and a great idea.

Log on to Github and find the repo for the server you're updating dlg-coreos is node-proxy, demography-website is demog-proxy.

Find the `index.js` file.  Open it, click on the pencil to edit it.

Change the numbers following each certificate type in the sslobj object to one digit higher.

Commit the change.

Log onto dockerhub.com, change to the codemog organization, find the proper repo, find the Build Details tab, wait until the most recent build is a success.

Even if you don't need to renew, having this done ahead of time shortens downtime to under a minute barring complications.
Now, move on to renewing the SSL.

## Now I need to renew the SSL certificate....

No problem.  This is really easy.  

SSH into the server that needs to be updated.

Then, run these commands (change out the proxy  and docker image based on the server).  This is why we run the dockerhub portion first, so we can do this immediately.

The certbot command will pull up a dialog screen and report back if it succeeded or not. If it freezes, see below. 

```
docker stop nodeproxy
docker rm nodeproxy
docker pull codemog/node-proxy 
docker rm certbot
docker run -it --rm -p 443:443 -p 80:80 --name certbot -v "/etc/letsencrypt:/etc/letsencrypt" -v "/var/lib/letsencrypt:/var/lib/letsencrypt" certbot/certbot renew
docker run --restart unless-stopped  --name nodeproxy -v /etc/letsencrypt/archive/gis.dola.colorado.gov:/ssl/docker --link demoglookup:demoglookup --link shiny-server:shiny-server --link censusmap:censusmap --link censusapi:censusapi --link muniapi:muniapi --link phantom:phantom --link cogrants:cogrants --link sdapi:sdapi --link pt2pl:pt2pl --link php:php -p 443:443 -p 80:80 -d codemog/node-proxy

OR

docker stop demogproxy
docker rm demogproxy
docker pull codemog/demog-proxy 
docker rm certbot
docker run -it --rm -p 443:443 -p 80:80 --name certbot -v "/etc/letsencrypt:/etc/letsencrypt" -v "/var/lib/letsencrypt:/var/lib/letsencrypt" certbot/certbot renew
docker run --restart unless-stopped  --name demogproxy -v /etc/letsencrypt/archive/demography.dola.colorado.gov:/ssl/docker --link website:website --link shiny-server:shiny-server -p 443:443 -p 80:80 -d codemog/demog-proxy
```

You should be up and running.


## Hey, docker commands aren't running

Congrats!  You're in the same spot I was in.  This didn't seem to have a cause, but docker died halfway through my work.

You'll need to reset the image from the Cloud Console, but FIRST, you'll need to unmount the `giant` disk that has our postgres data on it.  This is a precaution because they warn that file system corruption is a threat when resetting the image.

Run these commands (sudo -i puts you into an interactive sudo to give you auper user power!):

``` 
sudo -i

umount /giant

exit 
```

Then go to the console, click on the instance you're resetting, and click the "Reset" button from the top, click through the warning and wait.  Once it's done, log in and run `docker ps -a` to see what's running, everything should be back up.  Your database won't work though. You need to remount the drive, then recreate the docker data volume, then re-run the postgres container.  Use the commands below:

```
lsblk
--Check that the 850gb drive is still sdb, otherwise check what it is and change the line below.
cd /
mkdir giant
sudo -i
mount /dev/sdb /giant/
docker create -v /giant/pgdata:/var/lib/postgresql/data --name slowdata busybox
docker run --name postgres -p 5433:5432 -e POSTGRES_PASSWORD=whatever -d --volumes-from slowdata mdillon/postgis:9.4
```
it should work! You may need to remove slowdata and postgres before running the run and create above.
