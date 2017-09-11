# Demography Applications


### ACS Webmap 
- [Github (Client)](https://github.com/ColoradoDemography/CensusAPI_Map)
- [Github (Microservices)](https://github.com/ColoradoDemography/MS_CensusMap)
- [Application Link - 2015](https://demography.dola.colorado.gov/CensusAPI_Map_2015)
- [Application Link - 2014](https://demography.dola.colorado.gov/CensusAPI_Map)
- [Application Link - 2013](https://demography.dola.colorado.gov/CensusAPI_Map_2013)
- [Application Link - 2012](https://demography.dola.colorado.gov/CensusAPI_Map_2012)

### Age-Animation Bars
- Client Application
- [Github](https://github.com/ColoradoDemography/Age-Animation-Bars)
- [Application Link](https://demography.dola.colorado.gov/Age-Animation-Bars)

### Automatic Map Creator
- Client Application
- [Github]
- Application Links
  - [Counties in Colorado]
  - [States in USA]
  - [Countries in the World]

### Base Industries Pie Chart
- Client Application
- [Github](https://github.com/ColoradoDemography/CO_BaseIndustries)
- [Application Link](https://demography.dola.colorado.gov/CO_BaseIndustries)

### Broadband Status Map
- Client Application
- [Github](https://github.com/ColoradoDemography/D3_BroadbandStatus)
- [Application Link](https://dola.colorado.gov/gis-cms/content/interactive-broadband-map)

### Census Data Query Tool
- Client-Microservice Architecture
- [Github (Client)](https://github.com/ColoradoDemography/CensusAPI_Query_UI)
- [Github (Microservices)](https://github.com/ColoradoDemography/MS_CensusAPI)
- [Application Link](https://demography.dola.colorado.gov/CensusAPI_Query_UI)

### Census Data Timeseries
- Client-Microservice Architecture (TODO)
- [Github (Client)](https://github.com/ColoradoDemography/CensusAPI_Timeseries)
- [Github (Microservices)]
- [Application Link]

### Colorado DOLA Grants
- Client Application
- [Github](https://github.com/ColoradoDemography/CO_Grants)
- [Application Link]

### Colorado County Population Change (Bubbles)
- Client Application
- [Github](https://github.com/ColoradoDemography/Population-Bubbles)
- [Application Link](https://demography.dola.colorado.gov/Population-Bubbles)

### Colorado County Population Change (Animated Pie)
- Client Application
- [Github](https://github.com/ColoradoDemography/Animated-Pie)
- [Application Link](https://demography.dola.colorado.gov/Animated-Pie)

### Colorado Municipal Boundaries
- Client-Microservice Architecture (TODO)
- [Github (Client)](https://github.com/ColoradoDemography/CO_Muni)
- [Github (Microservices)] (TODO)
- [Application Link](https://demography.dola.colorado.gov/CO_Muni)

### Colorado Special Districts
- Client-Microservice Architecture (TODO)
- [Github (Client)](https://github.com/ColoradoDemography/CO_SpecialDistrict)
- [Github (Microservices)]
- [Application Link](https://demography.dola.colorado.gov/CO_SpecialDistrict)

### Colorado Unemployment Map
- Client Application
- [Github](https://github.com/ColoradoDemographyCO_BLS_Unemployment)
- [Application Link](https://demography.dola.colorado.gov/CO_BLS_Unemployment)

### Compare Cities (Likeness Tool)
- Client Application
- [Github](https://github.com/ColoradoDemography/CompareCities)
- [Application Link](https://demography.dola.colorado.gov/CompareCities)

### Demography Dashboard
- [Github (Shiny Application)](https://github.com/ColoradoDemography/demographic_dashboard)
- [Application Link](https://gis.dola.colorado.gov/apps/demographic_dashboard/)

### Net Migration Dashboard
- [Github (Shiny Application)](https://github.com/ColoradoDemography/netmigration_dashboard)
- [Application Link](https://gis.dola.colorado.gov/apps/netmigration_dashboard/)


### Demography Data Lookups
- Client-Microservice Architecture
- Jekyll Pages
- [Github (Client)](https://github.com/ColoradoDemography/Demog-Lookup-Clients)
- [Github (Microservices)](https://github.com/ColoradoDemography/MS_Demog_Lookups)
- Application Links
  - [Base Analysis](https://demography.dola.colorado.gov/economy-labor-force/data/base-analysis/)
  - [Components of Change](https://demography.dola.colorado.gov/births-deaths-migration/data/components-change/)
  - [County Demographic Profiles](https://demography.dola.colorado.gov/population/data/county-profile/)
  - [County Race by Age Forecast](https://demography.dola.colorado.gov/population/data/race-forecast/)
  - [County Single Year of Age](https://demography.dola.colorado.gov/population/data/county-sya/)
  - [County Single Year of Age Race Estimates](https://demography.dola.colorado.gov/population/data/race-estimate/)
  - [Household Projections](https://demography.dola.colorado.gov/housing-and-households/data/household-projections/)
  - [Jobs by Sector](https://demography.dola.colorado.gov/economy-labor-force/data/jobs-by-sector/)
  - [Labor Force Participation](https://demography.dola.colorado.gov/economy-labor-force/data/labor-force/)
  - [Municipal Population and Housing Estimates](https://demography.dola.colorado.gov/population/data/muni-pop-housing/)

### Map Gallery
- Client Application
- [Github](https://github.com/ColoradoDemography/CO_Map_Gallery)
- [Application Link](https://demography.dola.colorado.gov/CO_Map_Gallery)

### Migration Animation (Bubbles)
- Client Application
- [Github](https://github.com/ColoradoDemography/Migration-Bubbles)
- [Application Link](https://demography.dola.colorado.gov/Migration-Bubbles)

### Quadrant Chart
- Client Application
- [Github](https://github.com/ColoradoDemography/D3_Quadrant)
- [Application Link](https://demography.dola.colorado.gov/D3_Quadrant)

### Rural-Urban Commuting Areas (RUCA)
- Client Application
- [Github](https://github.com/ColoradoDemography/CO_RUCA)
- [Application Link](https://demography.dola.colorado.gov/CO_RUCA)

### Unemployment Chart
- Client Application
- [Github](https://github.com/ColoradoDemography/D3_Unemployment)
- [Application Link](https://demography.dola.colorado.gov/D3_Unemployment)


#### Architecture Descriptions

- **Client Application**s are purely static web applications with no server-side code dependancies.  Often the data is served in a CSV or JSON file along with the application code.  These applications are written in a mix of HTML, CSS, and Javascript.  These applications are served via Github Project Pages from their repository.
- **Client Application + Print** are like pure Client Applications, with the exception that they call a server process for print/save functionality.  In the event of server failure, these applications would still function without issue (aside from inabilty to save/print).  These applications are served via Github Project Pages from their repository.
- **Client-Microservice Architecture** are web applications that are written in HTML, CSS and Javascript, but which use AJAX calls to retrieve dynamic data from the web server (gis.dola.colorado.gov).   These applications are served via Github Project Pages from their repository, however they depend heavily on data from the server to function correctly.
- **Server Application**s are applications that are served directly from gis.dola.colorado.gov rather than Github (demography.dola.colorado.gov).  They can be written in any language.

