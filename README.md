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
