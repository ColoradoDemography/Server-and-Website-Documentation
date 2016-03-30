# CensusAPI_DB

## About the Colorado State Demography Office's Census Databases

**About**: This is a PostgreSQL/PostGIS Database Cluster with information at the State, County, Place, Tract, and Block Group Levels of Geography (and more) for the entire United States.  Currently, it includes data from the 1980, 1990, 2000 and 2010 Census, as well as the 2008-2012 5Y, and 2009-2013 5Y American Community Surveys.


The construction of each of the Census Databases was done with performance in mind.  It is designed specifically for mapping applications, where retrieving large volumes of spatial data quickly is a necessity.


Each Census Dataset is located in a separate database in the cluster.  Currently available are the 1980 Census (sf1 &amp; sf3), 1990 Census (sf1 &amp; sf3), 2000 Census (sf1 &amp; sf3), 2010 Census, 2008-2012 ACS, 2009-2013 ACS.


Because speed and data storage costs were a major concern, the data has been reduced down to only the most common geography levels.

- **1980**: State, County, Place, Tract, Block Group  (for 1980, Tract and Block Group data is not available nationwide)
- **1990**: State, County, Place, Tract, Block Group
- **2000**: State, County, Place, Tract, Block Group
- **2010**: State, County, Place, Tract, Block Group, ZCTA, SDUNI, SDELM, SDSEC, COUSUB
- **ACS 08-12**: State, County, Place, Tract, Block Group, ZCTA, SDUNI, SDELM, SDSEC, COUSUB
- **ACS 09-13**: State, County, Place, Tract, Block Group, ZCTA, SDUNI, SDELM, SDSEC, COUSUB
- **ACS 10-14**: State, County, Place, Tract, Block Group, ZCTA, SDUNI, SDELM, SDSEC, COUSUB


Geography sources available for each dataset:

- **1980**: [NHGIS](https://www.nhgis.org/) (State, County, Place, Tract - no Block Group)
- **1990**: [NHGIS](https://www.nhgis.org/), [Tiger Cartographic Boundaries](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html)
- **2000**: [Tiger Cartographic Boundaries](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html), [Tiger Shapefiles](https://www.census.gov/geo/maps-data/data/tiger-line.html)
- **2010**: [Tiger Cartographic Boundaries](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html), [Tiger Shapefiles](https://www.census.gov/geo/maps-data/data/tiger-line.html)
- **ACS 08-12**: [Tiger Cartographic Boundaries](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html), [Tiger Shapefiles](https://www.census.gov/geo/maps-data/data/tiger-line.html)
- **ACS 09-13**: [Tiger Cartographic Boundaries](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html), [Tiger Shapefiles](https://www.census.gov/geo/maps-data/data/tiger-line.html)
- **ACS 10-14**: [Tiger Cartographic Boundaries](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html), [Tiger Shapefiles](https://www.census.gov/geo/maps-data/data/tiger-line.html)


### Database Structure

Each database centers on the concept of a *geonum*.  A geonum is much like the census 'geoid' (or FIPS code), except, the geonum is an integer value that never begins with a leading '0'.  For instance, the census geoid for Denver County, Colorado would be the string '08031', while in our databases, the unique geonum would be the integer 108031.  For the basic geographies, the geonum is essentially the same as the geoid, but with a preceeding '1'.


Each database is divided into schemas.  Typically, there will be geographic schemas ('nhgis', 'carto', 'tiger'), table schemas ('sf1', 'sf3', or 'data') where the census data resides, and a search schema ('search').

Data can be retrieved from individual tables by joining from either geography, or from the search schema tables.

Example to select all tracts in Denver County, Colorado including Housing Units information (h1) using the search schema (c2010):

```SELECT * FROM search.data NATURAL JOIN data.h1 WHERE state=8 AND county=31 AND sumlev=140;```

Example to select all places in California, including Housing Units information (h1) using carto geography schema (c2010):

```SELECT * FROM carto.place NATURAL JOIN data.h1 WHERE state=6;```



