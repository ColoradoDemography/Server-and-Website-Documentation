# Demography Applications


### ACS Webmap 
- [Github (Client)](https://github.com/ColoradoDemography/CensusAPI_Map)
- [Github (Microservices)](https://github.com/ColoradoDemography/MS_CensusMap)
- [Application Link - 2020](https://gis.dola.colorado.gov/CensusAPI_Map_2021)
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

### Age-Animation Bars
- [Github](https://github.com/ColoradoDemography/Age-Animation-Bars)
- [Application Link](https://gis.dola.colorado.gov/Age-Animation-Bars)

### Age Distribution by County
- [Application Link](https://dola-online.maps.arcgis.com/apps/dashboards/713f5b5ecc4c4a7d85c6c266bba9131d)

### Base Industries Pie Chart
- [Github](https://github.com/ColoradoDemography/CO_BaseIndustries)
- [Application Link](https://gis.dola.colorado.gov/CO_BaseIndustries_Bar)

### BGU Viewer (2010)
- [Application Link](http://dola-online.maps.arcgis.com/apps/Solutions/s2.html?appid=2a869a4217ca40de891660504c0a3591)

### Bracketology
- [Github](https://github.com/ColoradoDemography/Bracketology)
- [Application Link](https://gis.dola.colorado.gov/Bracketology/)

### Broadband Status Map
- [Github](https://github.com/ColoradoDemography/D3_BroadbandStatus)
- [Application Link](http://coloradodemography.github.io/D3_BroadbandStatus/)

### Census Data Query Tool
- [Github (Client)](https://github.com/ColoradoDemography/CensusAPI)
- [Github (Microservices)](https://github.com/ColoradoDemography/MS_CensusAPI)
- [Application Link](https://gis.dola.colorado.gov/CensusAPI)

### Census Data Timeseries (non-functional)
- [Github (Client)](https://github.com/ColoradoDemography/CensusAPI_Timeseries)
- [Github (Microservices)]
- [Application Link]

### Census 2020 Interactive Map
- [Application Link](https://coloradodemography.github.io/Census_Data_2020/)

### Colorado DOLA Grants
- [Github](https://github.com/ColoradoDemography/CO_Grants)
- [Application Link](https://gis.dola.colorado.gov/CO_Grants)

### Colorado County Population Change (Bubbles)
- [Github](https://github.com/ColoradoDemography/Population-Bubbles)
- [Application Link](https://gis.dola.colorado.gov/Population-Bubbles)

### Colorado County Population Change (Animated Pie)
- [Github](https://github.com/ColoradoDemography/Animated-Pie)
- [Application Link](https://gis.dola.colorado.gov/Animated-Pie)

### Colorado Demographic Profiles
- [Application Link](https://gis.dola.colorado.gov/colorado-demographic-profiles/)

### Colorado Municipal Boundaries
- [Github (Client)](https://github.com/ColoradoDemography/CO_Muni)
- [Application Link](https://gis.dola.colorado.gov/CO_Muni)

### Colorado Municipal Data Map
- [Github](https://github.com/ColoradoDemography/Municipal_Data)
- [Application Link](https://coloradodemography.github.io/Municipal_Data/)

### Colorado Special Districts
- [Github (Client)](https://github.com/ColoradoDemography/CO_SpecialDistrict)
- [Application Link](https://gis.dola.colorado.gov/CO_SpecialDistrict)

### Colorado Unemployment Map
- Client Application
- [Github](https://github.com/ColoradoDemographyCO_BLS_Unemployment)
- [Application Link](https://gis.dola.colorado.gov/CO_BLS_Unemployment)

### Compare Cities (Likeness Tool)
- [Github](https://github.com/ColoradoDemography/CompareCities)
- [Application Link](https://gis.dola.colorado.gov/CompareCities)

### Components of Change Map
- [Github](https://github.com/ColoradoDemography/ComponentsOfChange)
- [Application Link](https://gis.colorado.gov/ComponentsOfChange)

### COVID Map Series
- [Application Link](https://arcg.is/mGPSK)

### Demography Dashboard
- [Github (Shiny Application - old version)](https://github.com/ColoradoDemography/demographic_dashboard)
- [Application Link](https://demography.dola.colorado.gov/assets/html/demodashboard.html)

### Density Map
- [Github](https://github.com/ColoradoDemography/Density_2020)
- [Application Link](https://gis.dola.colorado.gov/Density_2020/)

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

### Historical County Populations
- [Application Link](https://arcg.is/1KXX05)

### Historical Birthplaces of Colorado Residents
- [Application Link](https://public.flourish.studio/visualisation/3775693/)

### Historical Residence of Colorado Born
- [Application Link](https://public.flourish.studio/visualisation/3832584/)

### Job Change Map
- [Github](https://github.com/ColoradoDemography/Job_Change)
- [Application Link](https://gis.dola.colorado.gov/Job_Change/)

### Jobs and Migration
- [Github](https://github.com/ColoradoDemography/Jobs_Migration)
- [Application Link](https://gis.dola.colorado.gov/Jobs_Migration/)

### Job Sector Chart
- [Github](https://github.com/ColoradoDemography/Jobs_by_sector_chart)
- [Application Link](https://gis.dola.colorado.gov/Jobs_by_sector_chart)

### Job Sector County Map
- [Github](https://github.com/ColoradoDemography/Job_Sector_County)
- [Application Link](https://gis.dola.colorado.gov/Job_Sector_County)

### Map Gallery
- [Github](https://github.com/ColoradoDemography/WebsiteGrid/blob/main/assets/html/gis_applications.html)
- [Application Link](https://demography.dola.colorado.gov/assets/html/gis.html)

### Marijuana Grant Eligibility Map
- [Application Link](http://dola-online.maps.arcgis.com/apps/Viewer/index.html?appid=60c1688254fd4054bf5df1af8e7bc09f)

### Migration Animation (Bubbles)
- [Github](https://github.com/ColoradoDemography/Migration-Bubbles)
- [Application Link](https://gis.dola.colorado.gov/Migration-Bubbles)

### Net Migration Dashboard
- [Github (Shiny Application - old version)](https://github.com/ColoradoDemography/netmigration_dashboard)
- [Application Link](https://demography.dola.colorado.gov/assets/html/netmigcomp.html)

### Population Change by Age
-[Github](https://github.com/ColoradoDemography/AgeMap/)
-[Application Link](https://gis.dola.colorado.gov/AgeMap/)

### Poverty by Age
- [Github](https://github.com/ColoradoDemography/PovertyComprehensive)
- [Application Link](https://gis.dola.colorado.gov/PovertyComprehensive)

### Quadrant Chart
- [Github](https://github.com/ColoradoDemography/D3_Quadrant)
- [Application Link](https://gis.dola.colorado.gov/D3_Quadrant)

### Rural-Urban Commuting Areas (RUCA)
- [Github](https://github.com/ColoradoDemography/CO_RUCA)
- [Application Link](https://gis.dola.colorado.gov/CO_RUCA)

### SRF Disavantaged
- [Github](https://github.com/ColoradoDemography/disadvantaged_communities)
- [Application Link](https://gis.dola.colorado.gov/disadvantaged_communities/)

### Unemployment Chart
- [Github](https://github.com/ColoradoDemography/D3_Unemployment)
- [Application Link](https://gis.dola.colorado.gov/D3_Unemployment)

### Unemployment Ribbon
- [Application Link](https://gis.dola.colorado.gov/apps/unemployment_ribbon/)

### USDA Webmap
- [Application](https://dola.colorado.gov/gis-php/files/projects/USDA_Webmap/usda.html)


#### Architecture Descriptions (archive reference only)

- **Client Application**s are purely static web applications with no server-side code dependancies.  Often the data is served in a CSV or JSON file along with the application code.  These applications are written in a mix of HTML, CSS, and Javascript.  These applications are served via Github Project Pages from their repository.
- **Client Application + Print** are like pure Client Applications, with the exception that they call a server process for print/save functionality.  In the event of server failure, these applications would still function without issue (aside from inabilty to save/print).  These applications are served via Github Project Pages from their repository.
- **Client-Microservice Architecture** are web applications that are written in HTML, CSS and Javascript, but which use AJAX calls to retrieve dynamic data from the web server (gis.dola.colorado.gov).   These applications are served via Github Project Pages from their repository, however they depend heavily on data from the server to function correctly.
- **Server Application**s are applications that are served directly from gis.dola.colorado.gov rather than Github (demography.dola.colorado.gov).  They can be written in any language.

