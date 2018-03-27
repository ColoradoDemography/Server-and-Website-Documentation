# Update or Add Shiny-Aerver apps

We run two Shiny applications in production, the Demographic Dashboard and the Net Migration by Age Charts, both linked to on the homepage.  These two apps run differently than the rest of our applications in that they both run out of one Docker container, instead of each having their own.  This is in part because of how we developed it, but also due to the weight of the Shiny Docker container, we didn't want to have too many.  We also have used the survey to host apps that we need for a period of time, but don't need to be up all the time.

## How to updated existing applications

Because it's all in one container, we 'bash' into the Docker container then use `git pull` to update the applications.  An example of how to update the demographic dashboard is below.

```

docker exec -it shiny-server bash
cd /srv/shiny-server/demographic_dashboard
git pull
exit

```

This will open a bash session into the Docker container running Shiny Server (-i is interactive and -t sets tty).  Then we move to the application directory and use a `git pull` command to update the code. If you want to see what other apps are on the server run the code below, which goes into the main shiny directory and looks at the folders there.

``` 
docker exec -it shiny-server bash
cd /srv/shiny-server
ls -l

```

## How to add an application

The process here is very similar to updating, but uses a different git command.  

```

docker exec -it shiny-server bash
cd /srv/shiny-server/
git clone **URL FOR GITHUB REPO WITH APP IN IT***
exit

```

Then the app will be avaiable here: https://gis.dola.colorado.gov/apps/**FOLDER NAME**
The app uses that url based on how the node-proxy container is set up.

## Repulling Shiny Server Docker Container
Eventually automate this.
First some dependencies need to be loaded. Within the container run:
sudo apt-get install -y libxml2-dev libcurl4-openssl-dev libssl-dev (for tidyverse and kableExtra)
sudo apt-get install aptitude
sudo aptitude install libgdal-dev (for RPostgreSQL and rgdal)
Then go into R and run:
install.packages(c("dplyr","tidyr","plotly","readxl","scales","knitr","rmarkdown","shinydashboard","shinyjs","VennDiagram","gridExtra","tidyverse","kableExtra"))
devtools::install_github(c("ColoradoDemography/codemog","ColoradoDemography/codemogAPI","ColoradoDemography/codemogProfile","ColoradoDemography/codemogLib"))
## Hints and tricks

When adding a new app, all of its dependencies and libraries have to be included in the docker container.
The main app script needs to use either the app.R or ui.R and server.R convention.
