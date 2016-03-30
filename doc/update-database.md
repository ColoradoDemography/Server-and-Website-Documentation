## How to Add the Latest ACS Data

Every December, the US Census Bureau releases the latest vintage of the Amercian Community Survey 5-Year Database.  This is a core dataset used by the State Demography Database, and is featured prominently in our ACS Webmap.

The entire dataset for the US is massive.  For our purposes, we tend to only use a segment of the Summary Levels provided by the Census (State, County, Place, Tract, Block Group, ZCTA, SDUNI, SDELM, SDSEC, COUSUB - plus a few more).

Luckily, starting with the ACS 2010-2014, the process is no longer a manual process (it used to take a week).  However, you *will* need to make some obvious changes to the program code to enable it to access the most recent dataset. (Plus probably a few unforseen additional edits as well).

The program that extracts the ACS data and loads it into a database is located in a Github repository here: [https://github.com/royhobbstn/acs-processing](https://github.com/royhobbstn/acs-processing)

It has also been published as a command-line NPM package here:  [https://www.npmjs.com/package/acs1014](https://www.npmjs.com/package/acs1014)
(you may want to consider publishing a current version to the public after you get it working for yourself)

A couple of tips:

- Check out somefile.log if you're getting errors.
- The most obvious change you'll need to make is in the dl\_and\_extract.js file.
  - request('http://www2.census.gov/programs-surveys/acs/summary_file/2014/data/5_year_by_state/' + processing + geostring + '.zip')
  - You may need to change the entire link, or you may need to just replace the '2014' with '2015'
  - The Census may also have slightly altered the state filenames - check there if there are problems
- (I believe) the database needs to be created ahead of time.  You'll also need to make sure that any reference to 'acs104' is now 'acs105' (or whichever year)
- You'll want to run this on a temporary instance rather than the production server (please)
- This will take HOURS.  Make sure it will run correctly with one state or several small states before running it on the entire USA.
- Use the 'forever' module from npm to launch the task, or else you'll likely end up with timeout errors (or the agony of a timeout or fail on the very last state!)
- When completed, run pg\_dump, (use this format) ```pg_dump -Fc -h 104.197.26.248 -U postgres -p 5432 -d acs1115 > acs1115.custom```
- Then run pg\_restore on the production database (make sure the database exists first!) ```pg_restore -h 104.196.8.243 -p 5433 -U postgres -j 2 -d acs1115 /tmp/acs1115.custom```
- Don't delete the ```.custom``` file when you're done.  Save it in the ```census-database``` google storage bucket!
