# Writing a Dockerfile

**You probably shouldn't.**

If you're doing something simple like containerizing a nodejs app, go for it.  It is quite easy.

**If you're doing anything more complex than that, here are a few things you need to know:**

- Most of your problems will come from not having the right version of something, or missing a dependency of something else.

- You will need to learn how ```CMD``` and ```ENTRYPOINT``` work.  Don't gloss over this.

- Update and load all of your packages with one ```RUN``` command. ```&&``` is Linux-speak for ```and then do this``` ```&#92;``` is your way to tell Linux that you're continuing the command on the next line.

- You're in for a slightly agonizing method of development where you tweak one thing, build your instance, find you've solved that problem! (if you're lucky) and then have it fail again for a different reason.  Repeat 100x.  Then you're elated that your build was successful, but your image still doesn't work quite right.

- There aren't really that many commands to learn, so hop over to the [documentation page](https://docs.docker.com/engine/reference/builder/) and read about them all (There are only 16 commands - and many of them are going to be obviously irrelevant to your situation).  It won't take that long.  The struggle is in the details.

- Every command creates a new intermediate Docker container.  Anything in memory will dissapear.  This will be important to know BEFORE you start writing your first Dockerfile.

**Here is something that I'm not clear on:**

- When you're using another image as your base, what happens to the ```CMD``` and/or ```ENTRYPOINT``` commands from those containers if you specifiy your own ```CMD``` and/or ```ENTRYPOINT```?
