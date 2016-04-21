## About the Current Design

- Based on current dola design

## Layouts

- homepage

ONLY the main Demography homepage uses this layout.  Currently, the only difference from the 'page' template is the inclusion of the *infobox/infolinks* widget (the link box), and the presence or absence of the *data* button.

- page

Standard page template.  Includes the top bar (google translate), navigation, breadcrumbs, data button and footer.

- default

Both the *page* and *homepage* layout feeds into the *default* layout.  The *default* template wraps the *page* and *homepage* templates within an \<HTML\> tag, and adds the \<HEAD\> (including the meta elements and CSS and JS dependencies )

- compress





## Other Layout Pages

- redirect