


## Title

`rbefdata` - leveraging access to data and semantics

## Abstract

Today scientists need to deal with a deluge of data in many disciplines. While
there are some good and widely accepted tools that solve some of the most
pressing problems with data like their loss, other valuable concepts like for
example the use of meta data and formal representations of knowledge in form of
ontologies are not yet wide spread enough. This is related to the facts that
concepts can be hard to implement into data management solutions, the
reluctance of users towards new solutions, or a general lack of acceptance. We
here introduce the `rbefdata` package that links the R statistics environment
to the open source data management platform `BEFdata`.  The platform has been
developed and is used within the BEF-China experiment to manage the data. It is
specialized in the handling of small and heterogeneous data, which is
representing the majority of data in biodiversity research. We show the usage
of the package by creating a workflow in form of an R script.  The workflow
underlying analysis steps not only describe the interactions between the R
package and the data management platform but also reconstruct a facet of an
analysis where results have been published already.  We discuss the introduced
combination of software in the context of the data life cycle in ecology and
the current as well as future data management requirements.  Additionally, we
give an outlook on upcoming semantical assisted features like an improved
exploration of data and smart merging functionality to be integrated with
`rbefdata` and `BEFdata`.

## Introduction

* growing awareness of the value of data
* general reluctance to use and provide data to and from repositories
* at the same time a multitude of available data sources
* especially with small to medium sized datasets, scientists want to have the data
  at their fingertips, they want to use their own tools
* growing availability of workflow packages on R
* introducing the rbefdata package tailored to communicate with BEFdata
  repositories and tematres thesauri
* we demonstrate the usage with an interdisciplinary analysis on nutrient retention


With a growing awareness on the value of data, much effort has been put into
building data management platforms, that preserve all kinds of environmental
and historic data, (e.g. diversity workbench, GBIF, `BEFdata`, DataONE,
LifeWatch). Solutions emerged in different scientific disciplines that provide
data management plans for small scale projects as well as for large data
producing long term or remote sensing collaborations. An ongoing trend in that
context is the development of integrative databases and data platforms. They
serve as nodes that collect data from smaller databases of certain domains and
enable researchers to access a wide range of relevant data all from one place.
In fact, these platforms offer a solution to one of the most pressing problems
that we face with our valuable data today, their loss. Even tough this improves
the situation with preserving data there is still reluctance, as researchers
fear to give away and loose the control over their data.

With a growing global data pool the demand to use and reuse available data
grows as well. Especially in ecology the integration of small and heterogeneous
data offers the opportunity to answer questions on a much broader temporal and
spatial scale. Metadata is a crucial component for the effective reuse of data
as it improves its legibility. A plain dataset is hard to understand, to one
who is not familiar with it and it can be hard to decipher even by the author
itself, after some time has passed. For example it is hard to remember what
methods have been used to collect the data of a certain column or what the
abbreviations or the headers in the dataset mean. While metadata theoretically
solves the problem with undescribed data it is still hard to make researchers
use it extensively. This is closely related to the fact that it usually means
to learn new tools that help with the description process of data (e.g morpho,
dataUP).

To find relevant data in the growing pool of available data is a challenge.
While the extensive use of metadata (Metadata citations!) and the tagging with
keywords is a good start and in fact an essential part of the solution.
Nonetheless the process to decide on the relevance of data is still very time
and labour intensive. The integration of semantic resources like thesauri and
ontologies into data management and analysis tools offers a way to help
researchers not only to improve their search queries to find the relevant data
but also could be used in the process of integrating the data for analysis.
But ontology engineering and maintenance can be quite complex for certain
domains of knowledge that characterized by high heterogeneity introduced
through its interdisciplinary nature.

Additionally it can be error prone especially if analyses get more complex and
require the expertise of more than one research domain.  Formal representations
of knowledge like ontologies By developing tools which closely tie together
data management platforms, data exploration features, the access to data and
tools that help to describe data we can ensure an effective use and reuse of
data. Thus in this paper we want to introduce the new R package `rbefdata`
(https://github.com/befdata/rbefdata) which links the open source data
management platform `BEFdata` (https://github.com/befdata/befdata) to the R
statistics environment.  While the `BEFdata` platform offers sophisticated tool
to preserve, harmonize, describe and share data, the focus of the R package is
to provide tools to explore, understand and download the data for analysis, as
well as it offers functionality for uploading results back to the data
management platform.  `rbefdata` is innovative in that it provides data
together with metadata in the R environment. 


We showcase the functionality of the package available with version `0.3.5`
based on a workflow that integrates two datasets. The workflow reconstructs a
facet of an analysis that has been published by Lang et al. 2013. The analysis
is part of the BEF (Biodiversity and Ecosystem Functioning) - China experiment
and deals with data from the subproject called "pilot experiment".  It is a 15N
tracer experiment which aims to disentangle the effect of species mixtures on
system N retention. The workflow depicts how to ask for data access, how to
pull data into the R environment, the inspection of metadata and shows how to
upload data and attachments like figures and scripts back to the data
management platform.  


that R dataframes are
often restricted to the tabular information, but we use the attributes to
provide metadata together with thabular data!

Paper proposals are an emerging concept solving transparant data exchange and
reuse across disciplines and laboratories [citations!]

Introducing workflows, their merits, and ROpenSci. But also Kepler, Pegasus,
etc. Cite our paper on workflows.

 (http://ropensci.org/),
which is a community driven approach to wrap all science APIs and to create
solutions for R users to seamlessly pull data from different repositories
spread over the internet into R for analysis.

There is a need for tools at the fingertips of the researchers, that can be
easily integrated into their workflow and leverage their access to data as
well as semantic repositories.

## Material and Methods

### BEF-China 

The BEF - China project is a research collaboration consisting of 10-15
independent research groups, whose overarching aim is to disentangle the 'The
role of tree and shrub diversity for production, erosion control, element
cycling, and species conservation in Chinese subtropical forest ecosystems'.
The BEF-China project (www.bef-china.de) is funded by the German science
foundation (DFG, FOR 891) and uses two main research platforms located in the
provinces Jiangxi and Zhejiang in China (Bruelheide et al., 2012).  

### BEFdata portal

The [BEFdata](http://befdataproduction.biow.uni-leipzig.de/) platform is
specialized in managing small and heterogeneous data. It adheres to standards
like the Ecological Metadata Language (EML) and facilitates research
cooperation by a paper proposals tool. To create a paper proposal a researcher
can select datasets which are to be included in the analysis. Furthermore basic
information of the proposed paper such as the title, a rationale, the envisaged
journal and a date needs to be provided.  Sending in a proposal, a researcher
asks for access to the data and proposes his research idea to the project board
and data owners. The data owners get informed and can decide if and how they
like to participate in the upcoming paper or if they only like to get
acknowledged for providing their data (cite Karin). This process allows to
include or acknowledge all researchers involved in the data sampling process,
it promotes collaborations between research units and helps to avoid
duplication in publication initiatives on the same research ideas which adds to
the transparency of data publication. Finally the datasets assembled in a paper
proposal can be imported in one step to the R environment by `rbefdata`
package. Another strength of the `BEFdata` portal is the tagging functionality
for datasets and data columns which which his is also used in the `rbefdata`
package to explore datasets.

### Nutrient retention along a biodiversity gradient

In this paper we use an already published analysis on nutrient retention along
a biodiversity gradient as a use case to build a workflow that shows the
functionalities and inter linkages between the BEF-China data portal and the
`rbefdata` package. The analysis is typical for interdisciplinary sciences, as
it combines soil, taxon, and nutrient data. Data originating from field
campaigns of different collaborating laboratories and has to be merged prior to
analyses. 

'Knowledge of biodiversity effects on nutrient cycling patterns in subtropical
forest ecosystems is still very limited, particularly as regards macro
nutrients such as nitrogen and phosphorus. Experimental approaches using tree
saplings may promote an understanding of mechanisms that underlie nutrient
acquisition and cycling in early successional stages of secondary forests and
forest plantations. Insights in the potential of nutrient retention of young
tree plantations are of particular interest in China, where large areas have
been reforested in order to counteract soil erosion and to increase the soils’
water and nutrient retention capacity.  In this study we planted saplings of
four abundant early successional (evergreen and deciduous) tree species in
monoculture, two- and four-species combination to test the effect of species
richness on nitrogen acquisition and retention by using a 15N tracer
experiment. A crucial question in BEF research is the appropriate time scale of
experiments which allows species richness effects to emerge. This question
gains importance when long-lived and slowly growing organisms such as trees are
considered. We wanted to analyse whether species richness effects occur during
the establishment phase of early successional tree species typical of
subtropical forests of China.  More precisely we wanted to test the following
hypotheses: (H1) Nitrogen acquisition and retention increases with species
richness due complementary effects in species mixtures. (H2) Species richness
effects strengthen over time.' The respective proposal can be assessed under
(url) For a detailed description of the experimental design we refer to Lang et
al. 2013 

### rbefdata

The `rbefdata` package is open source software and the development takes place
on GitHub (https://github.com/befdata/befdata). The latest version can be
installed directly from the CRAN repository as usual, using the
`install.packages()` command. The `rbefdata` package started its development
within the BEF-China project and meanwhile is part of the rOpenSci project
(http://ropensci.org/). The rOpenSci project is a community driven approach to
give R users convenient access to many scientific data repositories. 

`rbefdata` enables access to the data and associated metadata stored on a
`BEFdata` platform. The metadata is provided attached to the data.frames of raw
data pulled from the platform. The package provides convenient methods to pull
single or multiple dataset into the R environment and offers functions that
help to upload final results datasets with the script attached that has been
used to derive the results from the original datasets which provides a valuable
insight into data provenance and also is a stepping stone for reproducible
research. 

On top of that it also integrates the access to vocabularies stored on
`tematres` servers which can be useful in exploring relevant data for an
analysis.


```r
install.packages("rbefdata")
```


## Example workflow 

We start setting up the R package, highlight the dataset exploration features
using an example that shows the inclusion the `tematres` vocabulary server
before we finally come to the processing of the data attached to the paper
proposal, the download of data as well as to the upload of final results.

### Setup `rbefdata`

After loading `rbefdata` into the working environment the settings need to be
set via the `bef.options()` command. A look into the options reveals several
fields that can be filled in. The most essential setting for the example
workflow we present here is the user credentials. These are used to
authenticate the user against the portal and to ensure the access to the data
has been granted as well as to log the data access. We need to set it as the
data is not yet open access at the time of writing. When it will be open access
in the near future, a key is no longer required to download the data.

Other options are the URLs to the `BEFdata` server instance and the `tematres`
vocabulary server as well as a field that stores the name of a download folder.
While the URL fields ensure the package communicates with the right servers the
download folder name is used to create a folder in case we download attached
files from a dataset or proposal. In our case there is no need to change the
URL to `BEFdata` server, as it defaults to the BEF-China instance that we use
to retrieve data from. If an own instance of the `BEFdata` portal or has been
set up, this URL needs to be changed so the package communicates with the right
server (see box below).


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





### Vocabulary integration 

A `tematres` server can hold different representations of formalized knowledge
like a thesaurus or even an ontology of a project. The `rbefdata` package
supports exploiting a `tematres` vocabulary server via the `rtematres` package.
We can find terms and relations as well as we can display their descriptions in
`rbefata`. This can be used to improve the exploration of datasets. For example
looking for datasets that deal with  "plant organs" we can display the
definition of that term first (box below). Then we ask the `BEFdata` portal for
datasets that are tagged with that term and we get back a few datasets. In a
next step we use the vocabulary on the `tematres` server to narrow down "plant
organs" and we find "leaf",  "root", "twig" as well as plural forms. We use the
narrower keywords to query the `BEFdata` server again for datasets associated
with them and get back all datasets associated with the narrower terms. This
can be used the other way around as well to restrict the datasets we get back
to higher order terms with `bef.tematres.api(task = "fetchUp", "plant organ")`.
 






















