# Folder Structure

FYI, if you use Prose.io as your primary means of editing the site, you may not see many of these folders.  Rest assured, they are there, and you can edit them via Github.
( See the main repository here: https://github.com/ColoradoDemography )

## \_data

This folder contains structured data files related to the layout of elements on the demography website.

*infobox.yml* This data document specifies the items in the infobox on the homepage.  If adding or subtracting links, be sure to follow the existing layout.

*language.yml* These are a series of text pieces that (are probably unnecessary and) allow you to customize certain text around your site.

## \_drafts

You can place unfinished, unpublished pages here.  Currently not being used.

## \_includes

This place *includes* all the page elements that go into your page.  For instance, there's an *include* for the navigation bar, the footer, the google translate functionality, etc.  Almost everything on your pages comes from these elements.  They are the building blocks that make up your page.

## \_layouts

A somewhat confusing (at first) hierarchy of page layout documents.  See the [layouts page](doc/layouts.md) for more information.

## \_posts

This is not currently used, but would be the place to put posts or news releases (if we ever want to start)

## \_site

Jekyll will crunch all of your markdown and html and YAML and Liquid, and the finished product will be your website (located here).  Note that the 'official' version is built by Github Pages via Jekyll running on Github's servers.  If you have a local repo and push to Github, the \_site folder is not being pushed (see .gitignore), only the raw materials.

## assets

Miscellaneous javascript, font, css files and more.

## dola\_assets

More miscellaneous javascript, css, and image files.  Probably should be combined with the folder above.

## geojson

GeoJSON files used to make maps are in this directory.

## images

The site's inline images are should be uploaded here.

## pages

All (most?) of your markdown content will be found in this folder.  

It is also meant to be a representation of the structure of the website:

- 0\_Homepage\_and\_Footer\_Links

These are all root level pages, meaning their URLs aren't based on a subdirectory (such as population or census-acs).  The homepage and basic site pages can be found here, including contact, credits, information, and the search page.  

The data subdirectory is the main data page for the State Demography Office.  All of the lookups are automatically populated here (via the magic of Liquid Templating), but additional data subjects such as Census Data Tools, GIS Data Downloads, and Thematic Maps are all linked from here.

- 1\_Population

Population Pages and Lookups.  All pages here have a URL structure under the /population/ subdirectory.

- 2\_BirthsDeathsMig

Formerly 'Components of Change'.  Birth, Death, and Migration pages and Lookups.  All pages here have a URL structure under the /births-deaths-migration/ subdirectory.

- 3\_EconomyLaborForce

Economy and Labor Force Pages and Lookups.  All pages here have a URL structure under the /economy-labor-force/ subdirectory.

- 4\_HousingHouseholds

Housing and Household Pages and Lookups.  All pages here have a URL structure under the /housing-and-households/ subdirectory.

- 5\_CensusACS

Pages dealing with Census and American Community Survey data and information.  All pages here have a URL structure under the /census-acs/ subdirectory.

- 8\_GIS

Yes, I know there isn't a GIS menu heading... but, there are enough related pages that fall naturally under this category.  All pages here have a URL structure under the /gis/ subdirectory.

- 9\_Not\_in\_Menu

Un-menued items are in this folder and have a directory listing under the /demography/ subdirectory.

- test

Put your crazy ideas here until they're ready for primetime.

