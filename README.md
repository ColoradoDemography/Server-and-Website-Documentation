
# Architecture of the Demography Website


### Why

The out-of-the-box CMS (content management system) that currently runs DOLA's website is not a good fit for the State Demography Office.  To aid in the understanding of demographic and economic trends and analysis, Demography relies upon dynamic visual and interactive content.  A new, non-CMS setup has been created to enable Demography to deliver this rich content.


### Philosophy

The current system setup was given a lot of thought and planning.  We tried to stick to several core principles.

- Ease of everyday use.
- Modularity
- Recoverability

##### Ease of Everyday Use

The website should be easy to update - by anyone.  Nobody should have to open up a command line prompt or IDE to create something simple like a block of text or to start a new page.

##### Modularity

To the extent possible, everything should be separate from everything else.  One bug or one failing application should not affect the entire system.  Applications should be able to come and go without leaving artifacts on the server.  Static files (HTML, CSS, Client-Javascript) should be separate from dynamically generated content (Server-side code).  A server crash should not be able to bring the whole website down.

##### Recoverability

In the event of a failure, it shouldn't take a week to re-create a new server and re-install all the components.  Every aspect of the system should be documented.


**With those principles in mind, our system was set up as follows:**


## CoreOS

We use a Google Compute Engine instance on Google Cloud Platform to run the dynamic content and applications on the website.  To put it simply, we have a computer in the 'cloud' which runs on a Linux operating system.  The 'flavor' of Linux we chose is called [CoreOS](https://coreos.com/).  CoreOS was elected for one main reason: it's an operating system that is built precisely for running 'containers' (more on that later).  It's a very light-weight operating system with few bells-and-whistles.  However, it comes with [Docker](https://www.docker.com/) pre-installed.  Every application and microservice is meant to run inside a container, rather than being installed on top of the operating system.


## PostgreSQL

Our database backend is Postgres.  This was by far our easiest technology choice; it's free, and it has fantastic support for spatial (GIS) capabilities with the PostGIS extension.


## Docker

Docker is the fundamental technology that drives our server-side architecture.  The ideal example of a Docker container is to run one 'service' or application only.  For instance, we have Docker containers for our Demography Dashboard, to lookup data from our database, and to schedule tasks such as downloading data weekly from an outside API.  Each of these containers is separate from each other (though the containers can 'talk amongst themselves' if we let them).

*Why is it important that these containers are separate from each other?*

Say that you wanted to add a new feature to your application.  But let's also say that for this new feature to work, you have to update some software first.
If you're running all of your applications together on one operating system, updating one piece of software can (and often does) have the side effect of 'breaking' something else that depends on an older version of that software.  However, when you run applications in isolated containers, the software update only affects that particular container.  The other containers can blissfully go on using their 'old' version of the software.

Modularity is also key in terms of employee continuity and general development flexibility.  Currently, the Demography Office has expertise in programming with Javascript and R.  If the current personnel get hit by a bus and are replaced by Java and Ruby developers, no problem!  Their applications can also be 'Dockerized' and launched into the same environment.  Additionally, the applications created by the 'departed' employees will still continue to run (and can easily be re-launched in the event of a server failure).


## Jekyll

Jekyll is a 'static' website creator.  Explained simply; you specify content (text, images, and links) and templates (the elements and structure) for your website, and Jekyll builds the site's pages for you.
Setting up a Jekyll site can be as easy or as hard as you want it to be.  On one end of the spectrum, you can start with pre-made templates and skip directly to generating content for your website.  On the other end, you can customize each and every aspect of presentation that you can imagine.
Needless to say, Demography customized the look of our custom Jekyll site to match that of DOLA's.  For us, it was important to have our customers feel as if they never left DOLA's web-pages (they haven't!).
General content (text, images, links, etc) for the site is written in a format called [markdown](https://guides.github.com/features/mastering-markdown/).  
This content can be written and committed directly to the [coloradodemography.github.io](https://github.com/ColoradoDemography/coloradodemography.github.io) repository without ever leaving Github.
However, one of our goals was 'ease of everyday use', and there is an easier way.  For most content creation, we use [prose.io](http://prose.io/). It provides a more classical WYSIWYG (what you see is what you get) interface to editing content, while subtly and inobtrusively teaching markdown at the same time (try it - you'll see what I mean).

Because Github doesn't currently support the combination of HTTPS and custom domains (as of 08/2016), it is necessary to self-host our Jekyll site rather than relying on Github pages (as was our original plan).  We're still hoping that Github will be able to support our configuration in the future, so we have structured our website (including static content from other [ColoradoDemography](https://github.com/ColoradoDemography) repositories) identically to how they would be if Github hosted them.

The server that hosts our website is set up nearly identically to that which hosts our microservices; it is a CoreOS server which consumes Docker containers.

The Docker container which servers our Jekyll site is a NodeJS & Ruby environment that is able to run the Jekyll build step, but can also serve the resulting static content using the [ExpressJS](https://expressjs.com/) framework.


## Microservices

So how do we combine the static content (Jekyll) with our dynamically generated content (the CoreOS-Docker Server)?  They appear to be two discrete entities (and they are).  The secret is in creating 'microservices'.
A microservice can be thought of as a relatively small program that does just one thing (and does it well), and is accessible through a URL endpoint.  This concept perfectly fits our idea of 'modularity'.  Rather than having one monolithic server-side application that handles every possible application request, you break down this functionality into a group of jobs (or processes) that need to be done.  Using my Census Map Application as an example; there is a process that retrieves GeoJson data for map display, a process that generates data for charts, a process that exports a csv table to a file - and it is all done by calling URL endpoints.

[See... clicking this link gives you data.](https://gis.dola.colorado.gov/lookups/profile?county=1&year=2011,2012&vars=births,deaths) This cryptic text may not mean much to you, but computers love to read it!

*Why use URL endpoints to deliver data?*

So that our Jekyll pages can access it by using [AJAX!](http://awaxman11.github.io/blog/2013/07/21/checking-out-js/) (client-side Javascript requests)  In this way, even though the static Jekyll pages cannot run any server scripts on their own, they can still access all the data they need through these URL's.  When you visit a data lookup, application, or a visualization, behind the scenes the Javascript on these Jekyll pages is calling a URL, processing the data, and turning ordinary HTML pages into something much more exciting!


## More Information

This was just a general overview.  To get into more detail on how everything works, click the links below for a deeper dive.  (This is also a note from present me to future me, so that you can quickly reconstruct or repair something if things go awry.)

- [Compute Engine CoreOS Instance Startup Guide](doc/server-setup.md)
  - [CoreOS Tips](doc/coreos-tips.md)
- Docker Containers
  - [Current Inventory and run instructions](doc/container-inventory.md)
  - [Useful Docker Commands](doc/docker-commands.md)
  - [Writing a Dockerfile](doc/writing-a-dockerfile.md)
  - [Schedule Container](doc/cron-container.md)
  - [Proxy Container](doc/proxy-container.md)
- [Google Storage Buckets](doc/google-storage-buckets.md)
- Jekyll Topics
	- [YAML](doc/yaml-musings.md)
  - [Folder Structure](doc/folder-structure.md)
  - [Layouts](doc/layouts.md)
  - [Includes](doc/includes.md)
  - [Data Lookup Applications](doc/lookups.md) 
  - [Index Pages](doc/index-pages.md)
- [Prose.io](doc/intro-to-prose-io.md)
  - [Guide to Creating a New Page](doc/create-a-page-proseio.md)
- [Style Guide](doc/style-guide.md)
- Applications
  - [Application Inventory](doc/application-directory.md)
  - [How to add an Application to demography.dola.colorado.gov?](doc/how-to-add-an-application.md)
- Database Documentation
  - [Overview (or, Why are there two database clusters?)](doc/database-overview.md)
  - [Census Databases schema](doc/census-db-schema.md)
  - [(An easy guide to) updating the Census Database](doc/update-database.md)
