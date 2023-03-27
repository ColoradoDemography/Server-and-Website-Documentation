
# YAML

**or... what's the deal with that weird stuff at the top of the page?**

YAML (also known as "Front Matter") are data elements that live at the top of every page that Jekyll processes.  (

**No YAML, No processing by Jekyll.**  YAML can be included in markdown or HTML pages (and more) to signify to Jekyll to process the file.

YAML currently stands for ("YAML Ain't Markup Language"). [Yes, really](https://en.wikipedia.org/wiki/YAML).  But in the past stood for ("Yet Another Markup Language").

YAML consists of a list of tags and values enclosed within a pair of triple-dash lines (---) like so:

```
---
layout: page
title: "Population Data"
permalink: "/population/"
description: "Population subject directory for the Colorado State Demography Office"
datalink: "/population/data"
---
```

Certain 'tags', like *layout*, *title*, and *permalink* are predefined, and have a specific meaning to Jekyll.  Other tags, like *datalink* are custom defined, and have specific context within certain pages.

## YAML in a Demography Website Context

Here's a guide to all the different YAML items you can define/edit for your Jekyll pages.

**Jeykyll Predefined YAML** (Mandatory)
```
layout: page
permalink: "/population/"
```
*What are they?*

**layout**: determines the layout used for the page.  Currently, the only options for this are 'page' and 'homepage'.  See the [layout](doc/layouts.md) page for more information.

**permalink**: determines the relative web page address (URL) for the page.  permalink: "/population/" would result in a URL of https://demography.dola.colorado.gov/population/ (The result of adding the base URL, https://demography.dola.colorado.gov + the permalink tag value.)

Layout and Permalink MUST Always be Included in YAML

**SDO-Specific YAML** (Mandatory)
```
title: "Population Data"
description: "Population subject directory for the Colorado State Demography Office"
```
*What are they?*

**title**: Creates the Title for the page, which is the text shown on individual browser tabs.  Additionally, this is a key tag for Search Engine Optimization.

**description**: A description of the contents of the page, also a key tag for Search Engine Optimization.  
Title and Description SHOULD Always be Included in YAML

**Other YAML Tags used for specific pages**
```
custom_js:
- /assets/js/FileSaver.min.js
file: "https://storage.googleapis.com/co-publicdata/county_profiles.csv"
years: "1985-2014"
tag: "popdata"
datalink: "/population/data"
subheadline: "HTTP 404"
teaser: "Maybe the webpage was moved or deleted; or did you maybe mistype the link?"
sitemap: false
fips: 08031
```
*What are they?*

**custom\_js**: Additional Javascript Script files can be loaded with this tag (in a list format - see above for example)

**file**: For Lookup pages. Specifies an associated data file and creates a hyperlink. 

**years**: Specifies the Year Range of the Dataset

**tag**: Allows a [Liquid Templating Language](https://shopify.github.io/liquid/) Script to locate this page (and include its data).  Used for data directory pages.

**datalink**: Specifies where the Data button link leads to.  If you don't want a data button, don't include this tag.

**sitemap**: Indicates the file should not be included in the sitemap. 

**fips**: The fips code of the geographic area that will be featured in the page (for community profile pages)


## Using YAML with Liquid

Liquid is a templating language that allows you to do some basic (but very cool and powerfull) operations on your webpage.

For instance, you could use Liquid to Look through all of your pages to find only those with a specific tag:
```
<ul>
{% assign pages_list = site.pages | sort: 'title' %}
  {% for page in pages_list %}
    {% if page.tag == "bdmdata" %}
      <br />
      <li><b><a href="{{ page.url }}">{{ page.title }}</a></b>&nbsp;&nbsp; {{ page.years }} </li>
      <p>
        <i>{{ page.description }}</i>
        <br /><br /> OR download: <a href="{{ page.file }}">{{ page.file | split: '/' | last }}</a>
      </p><hr>
    {% endif %}
  {% endfor %}
</ul>
```

At a very basic level (PLEASE see documentation), Liquid performs subsitutions.

For instance, Liquid would substitute the value {{page.years}} with whatever is specified in the YAML *years* tag for that particular page.
