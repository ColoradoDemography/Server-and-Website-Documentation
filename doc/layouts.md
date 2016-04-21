## About the Current Design

Our current design is a clone of the former [DOLA](https://www.colorado.gov/pacific/dola) (organization) style.  We recognize that many of our users identify with us strongly with DOLA, and to be taken to a website with a completely different look and feel would be jarring.  Within our current layout there is plenty of room for customization and optimization.  Thus far we have made minor style adjustments, and will continue to do so.


## Layouts

- homepage

ONLY the main Demography homepage uses this layout.  Currently, the only difference from the 'page' template is the inclusion of the *infobox/infolinks* widget (the link box), and the presence or absence of the *data* button.

- page

Standard page template.  Includes the top bar (google translate), navigation, breadcrumbs, data button and footer.

- default

Both the *page* and *homepage* layout feeds into the *default* layout.  The *default* template wraps the *page* and *homepage* templates within an \<HTML\> tag, and adds the \<HEAD\> (including the META elements and CSS and JS dependencies )

- compress

The *default* template feeds into the *compress* template.  This template is a brilliant creation of [Anatol Broder](http://anatol.penibelst.de/), check out the [documentation](https://github.com/penibelst/jekyll-compress-html)!  It minifies (removes whitespace) from your page so that you can serve a much leaner file to your user (and increase page speed)!



## Other Layout Pages

- redirect

Hopefully I won't have to use it for a while, but this will allow me to meta-equiv any moved pages.

