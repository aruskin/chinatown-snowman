Experimenting with [Snowman](https://github.com/glaciers-in-archives/snowman), a static site generator for SPARQL backends, to produce a prototype site for the Boston Research Center's [Chinatown Collections Survey Project](https://bostonresearchcenter.org/bringing-history-together-the-chinatown-collections-survey-project/). 

The SPARQL endpoint used for this site is for a custom Wikibase, currently only accessible through Northeastern University's VPN.

## How to generate the site

Install Snowman (see [Snowman repo](https://github.com/glaciers-in-archives/snowman) for fuller instructions)

To build from source: 
```
git clone https://github.com/glaciers-in-archives/snowman
cd snowman
go build -o snowman
```

Clone this repository:
```
git clone https://github.com/aruskin/chinatown-snowman.git
cd chinatown-snowman
```

Generate the static site files (you will need to be connected to the Northeastern University VPN to access the SPARQL endpoint specified in [snowman.yaml](snowman.yaml)):
```
[path to snowman directory]/snowman build
```

Serve the site locally:
```
[path to snowman directory]/snowman serve
```

##  How to navigate this repository

Look at the [Snowman](https://github.com/glaciers-in-archives/snowman) documentation for general information and guidance about the Snowman site repository structure.

At the top-level:

- [snowman.yaml](snowman.yaml): This is where the connection to the SPARQL endpoint is configured. Modify this if the endpoint URL changes. Keep in mind that the Wikibase Item and Property IDs used in the queries are tied to how those are defined in the Wikibase with the current SPARQL endpoint, so switching this out will have broader impacts. For example, if you used the Wikidata SPARQL endpoint, the query `select ?item where {?item wdt:P7 wd:Q21}` (which returns items with instance of human in the Chinatown Collections Wikibase) wouldn't return anything, because the [property with ID P7](https://www.wikidata.org/wiki/Property:P7) has been deleted.
- [views.yaml](views.yaml): This is where the connection between templates, queries, and views are defined. If you want to add a new page to the site, you'll need to set up a corresponding entry in this file. Pages that don't make use of the Wikibase data will still be generated via HTML templates and should have values for `output` and `template`, but not `query`.
- [queries](queries): This contains the SPARQL queries used to generate the content for the site; various HTML files in [templates](templates) make use of the results of these queries, based on the relationships between queries, templates, and views defined in [views.yaml](views.yaml). These are separated by the language in which results are returned, although the query logic is the same between languages otherwise. (In the future, may want to look into parameterizing the language code somehow.)
- [static](static): Right now, this only contains the stylesheet for the site, but in theory this is where you could put other static files (e.g., logos, Javascript)
- [templates](templates): This contains the HTML files used to generate the site. Subdirectories here:
    - [layouts](templates/layouts): This currently contains the base layouts that should apply to every page on the site; these are where the HTML head and body elements are defined (including language code, links to stylesheets, Javascript to get sortable DataTables to work).
    - [includes](templates/includes): This currently contains the English and simplified Chinese navbar and footer templates. Any other HTML templates that should be included in multiple pages should live here. 
    - [generic](templates/generic): This contains the templates for pages that don't need to be handled separately for the English and Chinese sides of the site (or that share enough logic that it makes more sense to handle the language-switching with conditional statements in the template)
    - [en](templates/en), [zh](templates/zh): These contain the templates for pages that are handled separately for the English and Chinese sides of the site (mostly static text pages).