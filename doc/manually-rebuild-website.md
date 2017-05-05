# Re-Build (update) The Website

The website it built on Jekyll, which takes the website repository and renders it into the website that everyone sees.  Github does this automatically for coloradodemography.github.io, but we need to run it on our server to re-build demography.dola.colorado.gov.

We use the [https://demography.dola.colorado.gov/Control-Panel/?authenticate=](https://demography.dola.colorado.gov/Control-Panel/?authenticate=) with our Github hash to authenticate.  This pulls up buttons that allow us to rebuild apps and the website as a whole. 

The problem is, it isn't very transparent and we may need to run it manually.  Have no fear, that's what this documentation is for.

## Process

It's fairly simple to rebuild the website by hand.  Run the following commmands in order after using ssh to connect to the demography-website server.

```
docker exec -it website bash
cd coloradodemography.github.io
git pull
jekyll build

```

That's it.  You should get a console message once it's rebuilt.
