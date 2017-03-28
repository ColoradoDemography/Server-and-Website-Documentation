## SSL Certificates seem important.  Do I need to renew them?

SSL Certificates are really important. They allow us to securely connect to our clients using https.  Generally, if you're asking you need to renew them.  Plus, running the renewal process will stop you if you don't.

## But first, dockerhub.com

I know this sounds weird, but you actually need to prep the last step before you start.  Actually, that sounds pretty normal and a great idea.

Log on to Github and find the repo for the server you're updating dlg-coreos is node-proxy, demography-website is demog-proxy.

Find the `index.js` file.  Open it, click on the pencil to edit it.

Change the numbers following each certificate type in the sslobj object to one digit higher.

Commit the change.

Log onto dockerhub.com, change to the codemog organization, find the proper repo, find the Build Details tab, wait until the most recent build is a success.

Now, move on to renewing the SSL

## Now I need to renew the SSL certificate....

No problem.  This is really easy.  

SSH into the server that needs to be updated.

Run these commands:

```
docker rm certbot

docker run -it --rm -p 443:443 -p 80:80 --name certbot -v "/etc/letsencrypt:/etc/letsencrypt" -v "/var/lib/letsencrypt:/var/lib/letsencrypt" quay.io/letsencrypt/letsencrypt:latest renew

```
That will pull up a dialog screen and report back if it succeeded or not.  

Then, run these commands (change out the proxy  and docker image based on the server)

```
docker stop nodeproxy
docker rm nodeproxy
docker pull codemog/node-proxy 
docker run --restart unless-stopped  --name nodeproxy -v /etc/letsencrypt/archive/gis.dola.colorado.gov:/ssl/docker --link demoglookup:demoglookup --link shiny-server:shiny-server --link censusmap:censusmap --link censusapi:censusapi --link muniapi:muniapi --link phantom:phantom --link cogrants:cogrants --link sdapi:sdapi --link pt2pl:pt2pl -p 443:443 -p 80:80 -d codemog/node-proxy

OR

docker stop demogproxy
docker rm demogproxy
docker pull codemog/demog-proxy 
docker run --restart unless-stopped  --name demogproxy -v /etc/letsencrypt/archive/demography.dola.colorado.gov:/ssl/docker --link website:website -p 443:443 -p 80:80 -d codemog/demog-proxy
```

You should be up and running.
