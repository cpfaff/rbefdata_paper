


## Title

`rbefdata` - leveraging access to data and semantics

## Abstract

In this paper we introduce the `rbefdata` package that provides the R
statistics environment with access to the open source data management platform
`BEFdata`. The R package leverages access to data and metadata, integrates a
semantic repository (thesaurus) and offers preservation for datasets and other
data products like scripts and figures. We showcase the functionality of the R
package and the interactions with the data management platform using an R
script. It pulls and analyses data associated with a research idea in form of a
paper proposal from the `BEFdata` instance of the BEF-China experiment. The
analysis in the workflow deals with N retention along a biodiversity gradient
and asks for the influence of biodiversity on the process. The results of the
analysis have been published already and thus the data used here is open
access. Thus the script and analysis presented here is fully reproducible by
executing the script. We discuss the introduced R package and the combination
of software in terms of the data life cycle and the current data management
requirements in ecology as well as we given an outlook on upcoming features of
`rbefdata` and `BEFdata`.

## Introduction 

Today ecologists face a deluge of data like in many other disciplines. This
puts much pressure on the development of tools that foster the preservation,
the exploration and the reuse of data. Many tools and concepts in data
management provide solutions to different parts of the life cycle of data.
However not all of them are widely spread or accepted throughout ecology. This
situation can be improved by the tight integration of data management concepts
into existing and widely used software and thus into the daily workflow of
researchers. Paper proposals and data provenance as ways to promote the
discussion of ideas and collaborations, metadata to improve data preservation
and information exchange as well as the integration of semantic resources to
enhance data exploration and processing, only represent a few examples of
valuable concepts with the potential to improve the progress of a data
intensive scientific domain like ecology. The `rbefdata` R package is an
approach to combine the strengths of the mentioned data management concepts
into a single and simple usable R package.

With a growing awareness on the value of data, many data management platforms
have been developed to preserve all kinds of environmental and historic data.
These provide data preservation for small scale projects as well as for large
scale, big data producing, long term or remote sensing collaborations (cite
e.g.  diversity workbench, `BEFdata`, DataONE, LifeWatch, Pangea, Bexis). An
ongoing trend in data preservation and accessibility is the development of
integrative databases or data portals (cite TRY, GBIF, Pangea). They serve as
nodes that collect data from smaller databases of a certain domain and enable
researchers to access a wide range of relevant data, all from one place. All
these platforms offer a solution to one of the most pressing problems in data
management the loss of valuable data (Heidorn, 2008). Even tough these
platforms improve the situation of data preservation, researchers are still
reluctant to use online data platforms as they fear to give away and loose the
control over their data (michener 2012). 

The demand to reuse available data grows with the amount of data available
(Heidorn, 2008). In ecology for example the reuse of data is of interest as the
integration of data offers the potential to answer questions on a much broader
temporal and spatial scale (michener, 2008). A problem with data reuse is that
available data is often not well described. Metadata gives researchers the
opportunity to describe their data and others to understand raw research data
even if they are not familiar with it (Fegraus 2005). Metadata is necessary as
plain primary research data can be hard to understand, and even hard to
decipher by the authors themselves after some time has passed. For example it
is hard to remember what methods have been used to collect the data of a
certain column or what the abbreviations and the headers in the dataset mean.
However metadata is still not used exhaustive as it usually always means to put
more time into the collected data and to learn new tools that help to describe
it (e.g morpho, dataUP).

To find relevant data for reuse is a challenging task that is getting even more
complex if more data gets available (Leinfelder et al, xxx). A common practice
in data discovery, next to full text search in data and metadata, is tagging
with keywords (Nadrowski 2013).  However a keyword search can be very coarse as
it may provide access to a set of data but misses other essential and relevant
data tagged with close related or synonymous keywords (Leinfelder et al. xxx,
michener 2008). For example a keyword search on "weight" and "leaves" will miss
datasets tagged only with "dry weight" or "wet weight" and "plant products"
that might be of interest as well.  The integration of semantic repositories
that provide taxonomies can potentially improve the situation here. These
repositories can embed the keywords into a hierarchical structure and so the
query can be extended along known relations of the search term (Leinfelder et
al.).

Before data can effectively be reused it may needs to be cleaned, imputed,
reshaped and merged. This usually takes up to 70% of an analysis script (Garijo
2012, Pfaff 2013 in prep). These preparatory steps are not only time and labour
intensive but also potentially error prone, especially if the amount and
complexity of data to be included increases. The integration of semantic
repositories that provide ontologies can help to solve these problems (michener
2008). As ontologies allow the machine readable access to knowledge of a
scientific domain they can be used to develop tools that "understand" the
contents of datasets and guide researchers on the process of data preparation.
While ontologies with a clear and small scope are very well used already (cite
xxx, e.g gene Ontology) it is a challenging tasks to create an ontology for
research domains like ecology that are characterized by a high degree of
interdisciplinarity (Parsons 2011). This characteristic leads to a
heterogeneous landscape of knowledge and concepts that would need to be covered
and formalized by the ontology.

We here introduce the `rbefdata` R package as companion to the open source data
management platform `BEFdata` (Nadrowski 2013). The package is part of the
rOpenSci (http://ropensci.org/) initiative which is a community driven project
to provide the R statistics environment (R Development Core Team 2008) with a
flexible access to scientific data repositories. The R package enables access
to data and metadata stored on a `BEFdata` platform, integrates semantic
repositories stored on `tematres` vocabulary servers
(http://www.vocabularyserver.com/) and provides data preservation functionality
for raw research data as well as for free format attachments files. We showcase
the functionality of the `rbefdata` package available with version 0.3.5. We
create a workflow in form of an R script that shows the semantic refinement of
keywords to improve the search of datasets, the use of metadata in data
processing, how to pull a complete set of data into the R environment based on
a paper proposal, and finally the upload of data products. The workflow is
created along an analysis about N retention that was done in the BEF-China
experiment. The results of the analysis have been published already and the
related data is open access (Lang et al.  2013) which makes the workflow shown
here fully reproducible. 

## Material and Methods 

### BEF-China 

The BEF (Biodiversity Ecosystem Functioning) - China project, funded by the
German Science Foundation (DFG, FOR 891) is a research collaboration consisting
of 10-15 independent research groups (www.bef-china.de). The overarching aim is
to disentangle the role of tree and shrub diversity for production, erosion
control, element cycling, and species conservation in Chinese subtropical
forest ecosystems. The project uses two main research platforms located in the
provinces Jiangxi and Zhejiang in China (Bruelheide et al., 2012).  

### BEFdata platform

The [BEFdata](http://befdataproduction.biow.uni-leipzig.de/) platform is has
been developed as part of the BEF-China experiment. It specialized in the
management of small and heterogeneous data that are typical for biodiversity
research. It offers data harmonization features, adheres to standards like
Ecological Metadata Language (EML) for metadata support and fosters the
exploration of data by keyword tagging and faceted search and faceted search
The platform facilitates research cooperations and the discussion of ideas by a
paper proposal tool. To create a paper proposal a researcher can select
datasets on the platform to be included in an analysis. Furthermore basic
information like a title, a rationale, the envisaged journal and a date needs
to be provided. Submitting a proposal, a researcher asks for access to the data
and proposes his research idea to the project board and the data owners. 

The data owners can decide if and how they like to participate in the upcoming
analysis or if they only like to get acknowledged for providing their data
(cite Karin). This process allows to include or acknowledge all researchers
involved in the data sampling process, it promotes collaborations between
research units and helps to avoid duplication in publication initiatives on the
same research ideas which adds to the transparency of data publication.
Finally all datasets assembled in a paper proposal can be imported into the R
environment by the `rbefdata` package. 

### The workflow: Nutrient retention along a biodiversity gradient

We use an analysis about N retention along biodiversity gradient in the
BEF-China experiment as a use case. We build a script that shows the
functionalities and inter linkages between the BEF-China data platform and the
`rbefdata` package. The analysis is typical for interdisciplinary research in
ecology, as it combines soil, taxon, and nutrient data where data originating
from field campaigns of different collaborating laboratories has to be merged
prior to analyses. A paper proposal based on 3 datasets with the title "Mixed
afforestations of young subtropical trees promote nitrogen acquisition and
retention" has been created. For a detailed rationale we refer to the paper
proposal on the `BEFdata` instance of the BEF-China portal (URL XX).

### rbefdata

The `rbefdata` package (GitHub: https://github.com/befdata/befdata) is a
companion to the open source data management platform `BEFdata`. The latest
stable version of `rbefdata` can be installed via the CRAN package repository.
`rbefdata` is part of the rOpenSci initiative (http://ropensci.org/) which aims
to provide the R statistics environment with packages that enable the seamless
access to scientific data repositories (cite rOpenSci). Basically the
`rbefdata` package enables access to data and metadata stored on a `BEFdata`
platform as well as it allows the upload of data products. The integration of a
`tematres` vocabulary server allows for an improved exploration of datasets.
The `tematres` vocabulary server can hold different representations of
vocabularies as it provides support for thesauri, taxonomies or ontologies. The
`rbefdata` package by default integrates the vocabulary of the BEF-China
experiment stored on a `tematres` server (url xxx). By the time of writing the
taxonomy on the server contains xxx terms used in biodiversity research. The
relations of terms provided by the `tematres` vocabulary can be used to improve
the search of relevant data for an analysis. 

## Example workflow 

### Setup `rbefdata`

The latest version of `rbefdata` is installed by the `install.packages()`
command. After the installation the package needs to be loaded into the working
environment with the `require()` (see box below).


```r
# load the package
require(rbefdata)

# list all options
bef.options()
```

```
## $url
## [1] "http://china.befdata.biow.uni-leipzig.de"
## 
## $tematres_url
## [1] "http://tematres.befdata.biow.uni-leipzig.de/vocab/index.php"
## 
## $tematres_service_url
## [1] "http://tematres.befdata.biow.uni-leipzig.de/vocab/services.php"
## 
## $download_dir
## [1] "downloads"
## 
## $user_credentials
## [1] ""
```


After that the options of the `rbefdata` package need to be set via the
`bef.options()` command.  A look into the options list reveals several fields
that can be filled in. The most essential setting for the example workflow we
present here is the user credentials. These are used to authenticate the user
against the platform and to ensure the access to the data has been granted as
well as to log the data access. We need to set it as the data is not yet open
access at the time of writing. When it will be open access in the near future,
a key is no longer required to download the data.

Other options are the URLs to the `BEFdata` server instance and the `tematres`
vocabulary server as well as a field that stores the name of a download folder.
While the URL fields ensure the package communicates with the right servers the
download folder name is used to create a folder in case we download attached
files from a dataset or proposal. In our case there is no need to change the
URL to `BEFdata` server, as it defaults to the BEF-China instance that we use
to retrieve data from. If an own instance of the `BEFdata` platform or has been
set up, this URL needs to be changed so the package communicates with the right
server (see box below).


```r
# querry a single option
bef.options("url")
```

```
## [1] "http://china.befdata.biow.uni-leipzig.de"
```



```r
# set credentials example
bef.options(user_credentials = "aölkjspoiul12")
```



```r
# set URL example
bef.options(url = "http://my.own.befdata.instance.com")
```





### Data discovery 

The `rbefdata` package supports exploiting a `tematres` vocabulary server via
the `rtematres` package.  We can find terms and relations as well as we can
display their descriptions in `rbefdata`. This can be used to improve the
exploration of datasets. For example looking for datasets that deal with
"plant organs" we can display the definition of that term first (box below).
Then we ask the `BEFdata` platform for datasets that are tagged with that term
and we get back a few datasets. In a next step we use the vocabulary on the
`tematres` server to narrow down "plant organs" and we find "leaf",  "root",
"twig" as well as plural forms. We use the narrower keywords to query the
`BEFdata` server again for datasets associated with them and get back all
datasets associated with the narrower terms. This can be used the other way
around as well to restrict the datasets we get back to higher order terms with
`bef.tematres.api(task = "fetchUp", "plant organ")`.
 

```r
# define the term plant organ
term_info = bef.tematres.api(task = "fetchNotes", "plant organ")
term_info
```

```
## $id
## [1] "74"
## 
## $term
## [1] "plant organ"
## 
## $language
## [1] "en"
## 
## $description
## [1] "In biology, an organ is a collection of tissues joined in a structural unit to serve a common function."
```

```r

# get datasets tagged with plant organ
datasets_plant_organ = bef.get.datasets_for_keyword("plant organ")
```

```
## Error: could not find function "bef.get.datasets_for_keyword"
```

```r
datasets_plant_organ
```

```
## Error: object 'datasets_plant_organ' not found
```

```r

# narrow down plant organ
narrow_tasks_plant_organ = bef.tematres.api(task = "fetchDown", "plant organ")
narrow_tasks_plant_organ
```

```
## $id
##  [1] "385"  "800"  "386"  "390"  "391"  "1336" "73"   "387"  "75"   "388"  "30"  
## 
## $term
##  [1] "flower"        "flower-head"   "flowers"       "fruit"         "fruits"       
##  [6] "inflorescence" "leaf"          "leaves"        "root"          "seed"         
## [11] "twig"
```

```r

# enrich the search with narrower keywords
datasets_plant_organ_narrow = bef.get.datasets_for_keyword(c(narrow_tasks_plant_organ$term))
```

```
## Error: could not find function "bef.get.datasets_for_keyword"
```

```r
datasets_plant_organ_narrow
```

```
## Error: object 'datasets_plant_organ_narrow' not found
```


### Download data 

The `rbefdata` package leverages data access through paper proposals by a
download function. It loads all associated datasets of a proposal into the R
environment in one single step.  It returns a list object that keeps a data
frame per list element containing a dataset of the proposal each (see box
below). The function requires the ID of the proposal to work, which can be
found in the URL (see box below).

![showcase_proposal](./figure/static/showcase_proposal.png)

* caption: The paper proposal in its final approved state. The information on that page
           contains a title, a rational an envisaged date and journal. The calculated authors
           and email lists for communication as well as the attached datasets and sub
           projects involved (only partially shown). The proposal is published alredy see 
           (Lang et al. 2013).

```
# the proposal URL shows the id is 90 
http://befdataproduction.biow.uni-leipzig.de/paperproposals/90
```





















