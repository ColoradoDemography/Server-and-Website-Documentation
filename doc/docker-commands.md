# Useful Docker Commands


Rather than using ```docker build ...``` all of our containers are created in Github repositories.  They are hosted on DockerHub, taking advantage of its ability to create an 'automated build' each time a repository is updated.

### The workflow

- Write some project code
- Push the code to Github
- Wait for DockerHub to test the automated build
- If successfull, log into the CoreOS machine
- Run ```docker pull codemog/imagename``` to update the image on your CoreOS instance
- Stop the previous version of the container ```docker stop name```
- Remove the previous version of the container ```docker rm name```
- Load the new container ```docker run ...```
- Jump for joy

### What do these ```docker run ...```  parameters mean?

```-d```  I've seen this described as 'daemon' or 'detached'.  It runs the process in the background.  The only reason (for you) not to use this is if you are testing a container on your development machine and need to see stdout (console messages) as it happens.

```--rm```  Use this if you want the container to 'clean up' after itself.  (You won't have to use ```docker rm name```)  I generally don't because if an error occurs, I like the container to stick around so I can look at the logs.

```-p x:y```  Containers each have a world of ports inside themselves.  This command maps a port on the container (y) to a port on the host (x).  I generally map the same container port to the same host port for clarity.  Note that if the port on the host isn't opened (in the firewall settings), you're not going to see your container directly from your browser to that mapped port.  That's generally what you want - the container should only be accessible through a proxy (more on that later), and you'll want to indirectly serve that through port 443 to pick up SSL and HTTPS.  

```--name containername```  Always use this.  Otherwise you'll be referring to your container by its ID, which is usually something like 'be5dae2c82e8'.

```-v /slow/pgdata:/var/lib/postgresql/data``` The -v parameter specifies a data path to mount from the host, to the container.  In the case of a database, this gives permanence to your data.  If you create a database inside a container, and that container exits, you've lost your data.  You would also use -v to mount super secret information into your docker container (you wouldn't want to commit your keyfiles in github and load them in that way!)

```mdillon/postgis:9.4``` This is usually the last item in a 'docker run' command.  (sometimes the last command can be an application or a shell script, but nevermind that for now).  The structure of this is: ```account/project:version```.  Leaving out ```:version``` defaults to ```:latest```.  Most of our containers use our own codemog account, and are thus formatted ```codemog/project```.

### Common Commands

**Pulling the newest version of a container**
```docker pull ...``` (it's a good habit to do this nearly every time you load or update a container)

**Starting a container**
```docker run ...``` (see above)

**Stopping a container**
```docker stop name```

**Stopping a stubborn container**
```docker kill name```

**Removing a container**
```docker rm name```

**Cleaning the Image Registry**

Do this occasionally, it will free up a lot of space on your hard drive.
```
docker rmi $(docker images --filter "dangling=true" -q --no-trunc)
```

**Retrieving Logs**
```docker logs name```  (anything written to stdout is visible here, like console.log statements and error messages)


**Shell into your container**
Hey, look!  It really is a computer within a computer!
```
docker exec -it containername bash
```

**Move into admin mode**
Some commands require admin privileges
```
sudo -i
```
