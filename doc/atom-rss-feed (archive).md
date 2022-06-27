# Using Atom (RSS-Like) Feed for the Crosstabs Blog

We use an Atom feed based on our blog to send out notifications to subscribers of an email list in MailChimp everytime we update it.

This is about the only time we use a plug in with jekyll, we use `jekyll-feed` to accomplish that.  The repo can be found [here](https://github.com/jekyll/jekyll-feed).

We needed to add a line to the `_config.yml` file that looks like this:

```
gems:
  - jekyll-feed
```

This will run when the site it built and automatically put an Atom feed at `https://demography.dola.colorado.gov/feed.xml`

I wouldn't change the path at this point, but you could do that if you wanted by adding a line like this to the `_config.yml`

```
feed:
  path: NEWPATH.xml
```

There are a ton of other options you can specify, check out the repo for more detailed instructions.  
