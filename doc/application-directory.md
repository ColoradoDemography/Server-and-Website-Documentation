# Demography Applications


### ACS Webmap 
- [Github (Client)](https://github.com/ColoradoDemography/CensusAPI_Map)
- [Github (Microservices)](https://github.com/ColoradoDemography/MS_CensusMap)
- [Application Link - 2021](https://gis.dola.colorado.gov/CensusAPI_Map_2021) *Current
- [Application Link - 2020](https://gis.dola.colorado.gov/CensusAPI_Map_2020)
- [Application Link - 2019](https://gis.dola.colorado.gov/CensusAPI_Map_2019)
- [Application Link - 2018](https://gis.dola.colorado.gov/CensusAPI_Map_2018)
- [Application Link - 2017](https://gis.dola.colorado.gov/CensusAPI_Map_2017)
- [Application Link - 2016](https://gis.dola.colorado.gov/CensusAPI_Map_2016)
- [Application Link - 2015](https://gis.dola.colorado.gov/CensusAPI_Map_2015)
- [Application Link - 2014](https://gis.dola.colorado.gov/CensusAPI_Map)
- [Application Link - 2013](https://gis.dola.colorado.gov/CensusAPI_Map_2013)
- [Application Link - 2012](https://gis.dola.colorado.gov/CensusAPI_Map_2012)
- [Application Link - 2011](https://gis.dola.colorado.gov/CensusAPI_Map_2011)
- [Application Link - 2010](https://gis.dola.colorado.gov/CensusAPI_Map_2010)

The ACS map is updated each year after the new ACS data is loaded into postgres, generally in January. Previously we created a new map for each year but starting with the 2017-2021 ACS we are making all years available within the application as a menu item in the 2nd button in the top left corner of the map.

To update this map to the newest year you will need to pull the github repository into your development environment. From there, add the new year into the index.html and change the initialize_cMap.js file to reflect the new acs database in the cMap.db variable. Then update webpack and push it back to github.

Adding more variables is pretty easy, those are done in the datatree.js and tableflavor.js, basically you add a json type item for each variable category. Look at other variables to get a sense of the proper format. The hardest part is finding the database table and column to draw the correct value.

The data is drawn from the data schema in the ACS database through the SDO Census API, the geography is drawn from the carto schema.

### Age-Animation Bars
- [Github](https://github.com/ColoradoDemography/Age-Animation-Bars)
- [Application Link](https://gis.dola.colorado.gov/Age-Animation-Bars)

### Age Distribution by County
- [Application Link](https://dola-online.maps.arcgis.com/apps/dashboards/713f5b5ecc4c4a7d85c6c266bba9131d)

Pretty simple line chart drawing from a table stored in ArcGIS Online. Just have to replicate the table with new data.

### Base Industries Bar Chart
- [Github](https://github.com/ColoradoDemography/CO_BaseIndustries)
- [Application Link](https://gis.dola.colorado.gov/CO_BaseIndustries_Bar)

Pulls data from the base analysis table via the demog lookup. For a new year, update the dates in the chart and update the startdata variable in app2.js to reflect the current year's data in Alamosa.

### BGU Viewer (2010)
- [Application Link](http://dola-online.maps.arcgis.com/apps/Solutions/s2.html?appid=2a869a4217ca40de891660504c0a3591)

Old application, haven't seen the need to update for 2020

### Bracketology
- [Github](https://github.com/ColoradoDemography/Bracketology)
- [Application Link](https://gis.dola.colorado.gov/Bracketology/)

Update as desired, March is a good time. To update, just go into the repository and update the population data in main.js

### Broadband Status Map
- [Github](https://github.com/ColoradoDemography/D3_BroadbandStatus)
- [Application Link](http://coloradodemography.github.io/D3_BroadbandStatus/)

Was an application to show the status of broadband plans implemented in rural Colorado. Likely obsolete at this point. Updates were made by changing the geojson files to show which maps each community should show up on.

### Census Data Query Tool
- [Github (Client)](https://github.com/ColoradoDemography/CensusAPI)
- [Github (Microservices)](https://github.com/ColoradoDemography/MS_CensusAPI)
- [Application Link](https://gis.dola.colorado.gov/CensusAPI)

Tool using the SDO Census API to allow users to obtain CSVs, jsons and geojson files for ACS tables. Once the new ACS database is loaded, a couple things need to be updated in the index.html in the repository. Add the option for the new ACS, make it selected and change $('$datasetl').val and loadtables to the new acs

### Census Data Timeseries (non-functional)
- [Github (Client)](https://github.com/ColoradoDemography/CensusAPI_Timeseries)
- [Github (Microservices)]
- [Application Link]

### Census 2020 Interactive Map
- [Application Link](https://gis.dola.colorado.gov/Census_Data_2020/)

Javascript map created using the ArcGIS Javascript API and pulling from data in ArcGIS Online. Will be adding more data categories as more 2020 Census data is released.

### Colorado DOLA Grants
- [Github](https://github.com/ColoradoDemography/CO_Grants)
- [Application Link](https://gis.dola.colorado.gov/CO_Grants)

Data is pulled from the grants.csv file in google cloud storage. That file is created from an R script that pulls the data from the Oracle database. I run this script at the beginning of every month. (need to put the script in github. The application itself is a webpack application and needs to be pushed to a developmental environment, updated, webpacked and pushed back to webpack. 

### Colorado County Population Change (Bubbles)
- [Github](https://github.com/ColoradoDemography/Population-Bubbles)
- [Application Link](https://gis.dola.colorado.gov/Population-Bubbles)

Simple D3 animation of the change of population among Colorado counties over the decades. To update, just add to the json file stored in datasets.js

### Colorado County Population Change (Animated Pie)
- [Github](https://github.com/ColoradoDemography/Animated-Pie)
- [Application Link](https://gis.dola.colorado.gov/Animated-Pie)

Simple D3 animation of the change of population among Colorado counties over the decades. To update, just add to the json file stored in flare.json

### Colorado Demographic Profiles
- [Application Link](https://gis.dola.colorado.gov/colorado-demographic-profiles/)

### Colorado Municipal Boundaries
- [Github (Client)](https://github.com/ColoradoDemography/CO_Muni)
- [Application Link](https://gis.dola.colorado.gov/CO_Muni)

Map to show the annexation data stored in postgres. The map itself pretty much never needs updating but the data is updated directly in postgres using QGIS. Will generally update a batch of annexations and then it is necessary to run postgis-transform.sql in pgadmin to update the muni boundary layer from the annexation changes. There are also shapefiles available to download from the application, these are created manually after running the sql program and then uploaded into google cloud.

### Colorado Municipal Data Map
- [Github](https://github.com/ColoradoDemography/Municipal_Data)
- [Application Link](https://gis.dola.colorado.gov/Municipal_Data/)

Application that we host for the Colorado Municipal League. Data is a geojson of the municipal boundaries with data on each municipality attached. CML will send new data yearly if there are any changes. Data is kept in K:\ProjectsMain\WebMaps\MuniInfoMap. Can make a new file with updated municipal boundaries if desired but it's not really necessary.

### Colorado Special Districts
- [Github (Client)](https://github.com/ColoradoDemography/Special_Districts_API)
- [Github (Client)](https://github.com/ColoradoDemography/CO_SpecialDistrict)
- [Application Link](https://gis.dola.colorado.gov/CO_SpecialDistrict)

Map showing the special districts in Colorado. Only those covered by Title 32 are included. All districts are maintained in postgres and updated using QGIS. We are limited by what the districts submit, so we do not have boundaries or current boundaries for all districts. New shapefiles for the different district types should also be created after major updates. The Special Districts API feeds the districts to the application.

### Colorado Unemployment Map
- [Github](https://github.com/ColoradoDemographyCO_BLS_Unemployment)
- [Application Link](https://gis.dola.colorado.gov/CO_BLS_Unemployment)

Map showing unemployment statistics by county from the Bureau of Labor and Statistics. BLS updates this data roughly monthly. Currently doing the pull using an R script that can be found at (https://github.com/ColoradoDemography/BLS_Unemployment_R). This creates a json file that then needs to be modified slightly. Found it easiest to do this in notepad, could probably modify the script to do it though. the [] at the ends and the / have to be deleted. Once ready, put this file in google cloud.

### Compare Cities (Likeness Tool)
- [Github](https://github.com/ColoradoDemography/CompareCities)
- [Application Link](https://coloradodemography.github.io/CompareCities)

Not being maintained at this time, a way to show a comparison of municipalities and CDPs in Colorado by 15 different factors.

### Components of Change Map
- [Github](https://github.com/ColoradoDemography/ComponentsOfChange)
- [Application Link](https://gis.dola.colorado.gov/ComponentsOfChange)

Map showing the number and rates of births, deaths and migration in counties between desired years. The data is drawn from our estimates database using the demog lookup. Changes have to be made in a development environment so that webpack can be applied. Changes to the data will be made automatically when new data is loaded into the database but the default year has to be changed within the program. This map also serves as the base architecture for the age and job change maps.

### COVID Map Series
- [Application Link](https://arcg.is/mGPSK)

Series of maps and charts in ArcGIS Online showing a variety of statistics about COVID and its impacts. Modifying this going into the future to be a more general dashboard.

### Demography Dashboard (old version)
- [Github (Shiny Application - old version)](https://github.com/ColoradoDemography/demographic_dashboard)
- [Application Link](https://demography.dola.colorado.gov/assets/html/demodashboard.html)

### Demography Dashboard (new version)
- [Github](https://github.com/ColoradoDemography/WebsiteGrid/blob/main/assets/html/demodashboard.html)
- [Application Link](https://demography.dola.colorado.gov/assets/html/demodashboard.html)

This is maintained inside the website repository now as a javascript application.

### Density Map
- [Github](https://github.com/ColoradoDemography/Density_2020)
- [Application Link](https://gis.dola.colorado.gov/Density_2020/)

ESRI Javascript API application showing the density of population and census block from the 2020 Census, also includes a swipe to compare against 2010. Blocks are generalized into categories by density so that the individual blocks don't have to be stored in ArcGIS Online.

### Demography Data Lookups
- [Github (Microservices)](https://github.com/ColoradoDemography/MS_Demog_Lookups)
- Application Links
  - [Base Analysis](https://gis.dola.colorado.gov/economy-labor-force/data/base-analysis/)
  - [Components of Change](https://gis.dola.colorado.gov/births-deaths-migration/data/components-change/)
  - [County Demographic Profiles](https://gis.dola.colorado.gov/population/data/county-profile/)
  - [County Race by Age Forecast](https://gis.dola.colorado.gov/population/data/race-forecast/)
  - [County Single Year of Age](https://gis.dola.colorado.gov/population/data/county-sya/)
  - [County Single Year of Age Race Estimates](https://gis.dola.colorado.gov/population/data/race-estimate/)
  - [Household Projections](https://gis.dola.colorado.gov/housing-and-households/data/household-projections/)
  - [Jobs by Sector](https://gis.dola.colorado.gov/economy-labor-force/data/jobs-by-sector/)
  - [Labor Force Participation](https://gis.dola.colorado.gov/economy-labor-force/data/labor-force/)
  - [Municipal Population and Housing Estimates](https://gis.dola.colorado.gov/population/data/muni-pop-housing/)

These all pull data from the estimates database in postgres via the demog lookup. Slowly replacing with new lookups within the website.

### Historical County Populations
- [Application Link](https://arcg.is/1KXX05)

Series of maps showing Colorado's counties and their populations through history.

### Historical Birthplaces of Colorado Residents
- [Application Link](https://public.flourish.studio/visualisation/3775693/)

Application hosted in Flourish to show what states Colorado residents were born in through history. Need the Flourish login to access

### Historical Residence of Colorado Born
- [Application Link](https://public.flourish.studio/visualisation/3832584/)

Application hosted in Flourish to show where people born in Colorado have lived through history. Need the Flourish login to access

### Job Change Map
- [Github](https://github.com/ColoradoDemography/Job_Change)
- [Application Link](https://gis.dola.colorado.gov/Job_Change/)

Map showing the change in the number of jobs in counties between desired years. The data is drawn from our estimates database using the demog lookup. Changes have to be made in a development environment so that webpack can be applied. Changes to the data will be made automatically when new data is loaded into the database but the default year has to be changed within the program.

### Jobs and Migration
- [Github](https://github.com/ColoradoDemography/Jobs_Migration)
- [Application Link](https://gis.dola.colorado.gov/Jobs_Migration/)

Bar and line chart showing job change and migration by year for all counties. Both pieces of data are pulled from our estimates database using the demog lookup. Nnew years have to be added within the repository in app.js

### Job Sector Chart
- [Github](https://github.com/ColoradoDemography/Jobs_by_sector_chart)
- [Application Link](https://gis.dola.colorado.gov/Jobs_by_sector_chart)

### Job Sector County Map
- [Github](https://github.com/ColoradoDemography/Job_Sector_County)
- [Application Link](https://gis.dola.colorado.gov/Job_Sector_County)

Map to show job sectors by county, both total and percent. Pulls data from a version of the jobs table that is specifically created for this chart by taking the original jobs table in the postgres estimates database and replacing all nulls with 0 and creating the new table called jobs0. This application has to be updated in a development environment due to using webpack. The queried years variable in workers/load_data.js has to be updated each yearas well as variables in three of the other javascript files (add_title_control.js, get_from_dom.js and init_object.js).

### Map Gallery
- [Github](https://github.com/ColoradoDemography/WebsiteGrid/blob/main/assets/html/gis_applications.html)
- [Application Link](https://demography.dola.colorado.gov/assets/html/gis.html)

This is where we maintain the list of publically released visualizations

### Marijuana Grant Eligibility Map
- [Application Link](http://dola-online.maps.arcgis.com/apps/Viewer/index.html?appid=60c1688254fd4054bf5df1af8e7bc09f)

Map of counties eligible for marijuana grants. Hasn't been updated in quite awhile, based upon the needs of https://cdola.colorado.gov/funding-programs/marijuana-enforcement-grant

### Migration Animation (Bubbles)
- [Github](https://github.com/ColoradoDemography/Migration-Bubbles)
- [Application Link](https://coloradodemography.github.io/Migration-Bubbles)

Old visualization of migration to and from Colorado based upon 2006-2010 ACS data. Hasn't been updated as it's not particularly useful, need a better version at some point. Migration data is rather lacking currently due to survey issues around the pandemic.

### Net Migration Dashboard
- [Github (Shiny Application - old version)](https://github.com/ColoradoDemography/netmigration_dashboard)
- [Application Link](https://demography.dola.colorado.gov/assets/html/netmigcomp.html)

### Population Change by Age
-[Github](https://github.com/ColoradoDemography/AgeMap/)
-[Application Link](https://gis.dola.colorado.gov/AgeMap/)

Map showing the change in population by age in Colorado counties between the selected years. Draws from the county_sya table in the estimates database through the demog lookup. Large data pull, thus the long initialization time. This application has to be updated in a development environment due to using webpack. The load_data.js and add_custom_control.js have to be updated each year.

### Poverty by Age
- [Github](https://github.com/ColoradoDemography/PovertyComprehensive)
- [Application Link](https://gis.dola.colorado.gov/PovertyComprehensive)

Map showing poverty levels for different age groups based upon ACS 5 year data. Built using ArcGIS Javascript API version 3. The data is stored in ArcGIS Online. Uses data from ACS table B17024, probably easiest to download all census tract data from our API, then change the column headings to match what was used the previous year.

### Quadrant Chart
- [Github](https://github.com/ColoradoDemography/D3_Quadrant)
- [Application Link](https://coloradodemography.github.io/D3_Quadrant)

Not being used currently but an interesting application that compares counties or states on up to 3 variables at once from the ACS. May be worth reviving?

### Rural-Urban Commuting Areas (RUCA)
- [Github](https://github.com/ColoradoDemography/CO_RUCA)
- [Application Link](https://gis.dola.colorado.gov/CO_RUCA)

### SRF Disavantaged
- [Github](https://github.com/ColoradoDemography/disadvantaged_communities)
- [Application Link](https://gis.dola.colorado.gov/disadvantaged_communities/)

### Unemployment Chart
- [Github](https://github.com/ColoradoDemography/D3_Unemployment)
- [Application Link](https://gis.dola.colorado.gov/D3_Unemployment)

Chart showing unemployment statistics by county from the Bureau of Labor and Statistics. BLS updates this data roughly monthly. Currently doing the pull using an R script that can be found at (https://github.com/ColoradoDemography/BLS_Unemployment_R). This creates a json file that then needs to be modified slightly. Found it easiest to do this in notepad, could probably modify the script to do it though. the [] at the ends and the / have to be deleted. Once ready, put this file in google cloud. The length of the chart needs to be extended in the program with each new year.

### Unemployment Ribbon
- [Application Link](https://gis.dola.colorado.gov/apps/unemployment_ribbon/)

### USDA Webmap
- [Application](https://dola.colorado.gov/gis-php/files/projects/USDA_Webmap/usda.html)


#### Architecture Descriptions (archive reference only)

- **Client Application**s are purely static web applications with no server-side code dependancies.  Often the data is served in a CSV or JSON file along with the application code.  These applications are written in a mix of HTML, CSS, and Javascript.  These applications are served via Github Project Pages from their repository.
- **Client Application + Print** are like pure Client Applications, with the exception that they call a server process for print/save functionality.  In the event of server failure, these applications would still function without issue (aside from inabilty to save/print).  These applications are served via Github Project Pages from their repository.
- **Client-Microservice Architecture** are web applications that are written in HTML, CSS and Javascript, but which use AJAX calls to retrieve dynamic data from the web server (gis.dola.colorado.gov).   These applications are served via Github Project Pages from their repository, however they depend heavily on data from the server to function correctly.
- **Server Application**s are applications that are served directly from gis.dola.colorado.gov rather than Github (demography.dola.colorado.gov).  They can be written in any language.

