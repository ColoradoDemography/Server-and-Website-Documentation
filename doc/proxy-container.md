
# Proxy-Container

In order for all Docker container services to be SSL enabled and accessible without having to specify a port address, we utilize a proxy container.  The node [Redbird](https://github.com/OptimalBits/redbird) library makes this implementation detail trivial.

To add a container to the proxy, add a line to the end of the file like so:

```
redbird.register('gis.dola.colorado.gov/sd', 'http://sdapi:4006', {ssl: true});
```

The only moving parts to this line of code are:

```
/sd
```
The URL directory path where all your addresses will be located.  So, if in your api you specified a route '/lookups?', then it will now be publicly accessible (with SSL) through /sd/lookups?

```
sdapi
```
This is the container name you specify in your 'docker run...' command.

```
4006
```
This is the port that the container is running on.  It does not have to be an open port (since it will be proxied to 443).