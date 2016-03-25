# Demography Applications


### ACS Webmap 
- Client-Microservice Architecture
- [Github (Client)](https://github.com/royhobbstn/CensusAPI_Map)
- [Github (Microservices)](https://github.com/royhobbstn/MS_CensusMap)
- [Application Link](https://coloradodemography.github.io/CensusAPI_Map)

### Age-Animation Bars
- Client Application
- [Github](https://github.com/royhobbstn/Age-Animation-Bars)
- [Application Link](https://coloradodemography.github.io/Age-Animation-Bars/agebars.html)

### Automatic Map Creator
- Client Application
- [Github]
- Application Links
  - [Counties in Colorado]
  - [States in USA]
  - [Countries in the World]

### Base Industries Pie Chart
- Client Application
- [Github](https://github.com/royhobbstn/CO_BaseIndustries)
- [Application Link](https://coloradodemography.github.io/CO_BaseIndustries)

### Broadband Status Map
- Client Application
- [Github](https://github.com/royhobbstn/D3_BroadbandStatus)
- [Application Link](https://dola.colorado.gov/gis-cms/content/interactive-broadband-map)

### Census Data Query Tool
- Client-Microservice Architecture
- [Github (Client)](https://github.com/royhobbstn/CensusAPI)
- [Github (Microservices)](https://github.com/royhobbstn/MS_CensusAPI)
- [Application Link](https://coloradodemography.github.io/CensusAPI/queryapi.html)

### Census Data Timeseries
- Client-Microservice Architecture (TODO)
- [Github (Client)](https://github.com/royhobbstn/CensusAPI_Timeseries)
- [Github (Microservices)]
- [Application Link]

### Colorado DOLA Grants
- Client Application
- [Github](https://github.com/royhobbstn/CO_Grants)
- [Application Link]

### Colorado County Population Change (Bubbles)
- Client Application
- [Github](https://github.com/royhobbstn/Population-Bubbles)
- [Application Link](https://coloradodemography.github.io/Population-Bubbles/allpop2.html)

### Colorado County Population Change (Animated Pie)
- Client Application
- [Github](https://github.com/royhobbstn/Animated-Pie)
- [Application Link](https://coloradodemography.github.io/Animated-Pie/pop_pie.html)

### Colorado Municipal Boundaries
- Client-Microservice Architecture (TODO)
- [Github (Client)](https://github.com/royhobbstn/CO_Muni)
- [Github (Microservices)] (TODO)
- [Application Link](https://coloradodemography.github.io/CO_Muni)

### Colorado Special Districts
- Client-Microservice Architecture (TODO)
- [Github (Client)](https://github.com/royhobbstn/CO_SpecialDistrict)
- [Github (Microservices)]
- [Application Link](https://coloradodemography.github.io/CO_SpecialDistrict)

### Colorado Unemployment Map
- Client Application
- [Github](https://github.com/royhobbstn/CO_BLS_Unemployment)
- [Application Link](https://coloradodemography.github.io/CO_BLS_Unemployment)

### Compare Cities (Likeness Tool)
- Client Application
- [Github](https://github.com/royhobbstn/CompareCities)
- [Application Link](https://coloradodemography.github.io/CompareCities)

### Demography Dashboard
- Server Application
- [Github]
- [Application Link]

### Demography Data Lookups
- Client-Microservice Architecture
- Jekyll Pages
- [Github (Client)](https://github.com/royhobbstn/Demog-Lookup-Clients)
- [Github (Microservices)](https://github.com/royhobbstn/MS_Demog_Lookups)
- Application Links
  - [Base Analysis](http://coloradodemography.github.io/economy-labor-force/data/base-analysis.html)
  - [Components of Change](http://coloradodemography.github.io/births-deaths-migration/data/components-change.html)
  - [County Demographic Profiles](http://coloradodemography.github.io/population/data/county-profile.html)
  - [County Race by Age Forecast](http://coloradodemography.github.io/population/data/race-forecast.html)
  - [County Single Year of Age](http://coloradodemography.github.io/population/data/county-sya.html)
  - [County Single Year of Age Race Estimates](http://coloradodemography.github.io/population/data/race-estimate.html)
  - [Household Projections](http://coloradodemography.github.io/housing-and-households/data/household-projections.html)
  - [Jobs by Sector](http://coloradodemography.github.io/economy-labor-force/data/jobs-by-sector.html)
  - [Labor Force Participation](http://coloradodemography.github.io/economy-labor-force/data/labor-force.html)
  - [Municipal Population and Housing Estimates](http://coloradodemography.github.io/population/data/muni-pop-housing.html)

### Map Gallery
- Client Application
- [Github](https://github.com/royhobbstn/CO_Map_Gallery)
- [Application Link](https://coloradodemography.github.io/CO_Map_Gallery)

### Migration Animation (Bubbles)
- Client Application
- [Github](https://github.com/royhobbstn/Migration-Bubbles)
- [Application Link](https://coloradodemography.github.io/Migration-Bubbles/ptmigration.html)

### Quadrant Chart
- Client Application
- [Github](https://github.com/royhobbstn/D3_Quadrant)
- [Application Link](https://coloradodemography.github.io/D3_Quadrant)

### Rural-Urban Commuting Areas (RUCA)
- Client Application
- [Github](https://github.com/royhobbstn/CO_RUCA)
- [Application Link](https://coloradodemography.github.io/CO_RUCA)

### Unemployment Chart
- Client Application
- [Github](https://github.com/royhobbstn/D3_Unemployment)
- [Application Link](https://coloradodemography.github.io/D3_Unemployment)


#### Architecture Descriptions

- **Client Application**s are purely static web applications with no server-side code dependancies.  Often the data is served in a CSV or JSON file along with the application code.  These applications are written in a mix of HTML, CSS, and Javascript.
- **Client Application + Print** are like pure Client Applications, with the exception that they call a server process for print/save functionality.
- **Client-Microservice Architecture** are web applications who are written in HTML, CSS and Javascript, but which use AJAX calls to retrieve dynamic data from the web server (gis.dola.colorado.gov)
- **Server Application**s are applications that are served directly from gis.dola.colorado.gov rather than Github (demography.dola.colorado.gov).  They can be written in any language.

