


## Title

`rbefdata` - leveraging access to data and semantics

## Abstract

Today ecologists face a deluge of data like in many other disciplines. This
puts much pressure on the development of tools that foster the preservation of
data as well as the exploration and reuse of available data. Many tools and
concepts available in data management provide solutions to different parts of
the data life cycle. However not all of them are widely spread or accepted
throughout ecology. This situation can be improved by the tight integration of
data management concepts into existing and widely used software and thus into
the daily workflow of researchers. Paper proposals and data provenance as ways
to promote the discussion of ideas and collaborations, metadata to improve data
preservation and information exchange as well as the integration of semantic
resources to enhance data exploration and processing. These represent only a
few examples of valuable concepts with the potential to improve the progress of
a data intensive scientific domain like ecology. 

In this paper we introduce the `rbefdata` package that provides the R
statistics environment with access to the open source data management platform
`BEFdata`. The R package leverages access to data and metadata, includes the
integration of a semantic repository and offers preservation functionality for
datasets and other data products like free format attachment files. We showcase
the functionality of the R package and the interactions with the data
management platform using an R script workflow. It pulls and analyses data
associated with a paper proposal from the `BEFdata` instance of the BEF-China
experiment. The analysis in the workflow deals with N retention along a
biodiversity gradient. The results of the analysis itself have been published
already and thus the data used here is open access. This makes the workflow
script presented, fully reproducible by executing the script step by step. We
discuss the introduced R package and the combination of software in terms of
the data life cycle and the current data management requirements in ecology as
well as we given an outlook on upcoming features of `rbefdata` and `BEFdata`.

## Introduction

With a growing awareness on the value of data, many data management platforms
have been developed that preserve all kinds of environmental and historic data.
These provide data preservation plans for small scale projects as well as for
large scale, big data producing, long term or remote sensing collaborations
(e.g. diversity workbench, `BEFdata`, DataONE, LifeWatch). An ongoing trend in
data preservation and accessibility is the development of integrative databases
or data portals (TRY, GBIF). They serve as nodes that collect data from smaller
databases of a certain domain and enable researchers to access a wide range of
relevant data, all from one place. All these platforms offer a solution to one
of the most pressing problems that we face with our valuable data today, their
loss (cite xxx). Even tough this improves the situation in data preservation,
there is still reluctance of researchers to use online data platforms as they
fear to give away and loose the control over their data (cite xxx). 

The demand to reuse the available data grows with the amount of data available.
In ecology for example the reuse of data is of particular interest as the
integration of data offers the potential to answer questions on a much broader
temporal and spatial scale (cite xxx). A problem on data reuse is that
available data is often not well described. Metadata solves this problem and
gives researchers the opportunity to describe their data and others to
understand raw research data even if they are not familiar with it. Metadata is
necessary as plain primary research data can be hard to understand, and even
hard to decipher by the authors themselves after some time has passed. For
example it is hard to remember what methods have been used to collect the data
of a certain column or what the abbreviations and the headers in the dataset
mean. However metadata is still not used extensively as it usually means more
to put more time into data and to learn new tools that help to describe (e.g
morpho, dataUP).

To find relevant data for reuse is a challenging task that is getting even more
complex when more data gets available. A common practice in data discovery,
next to full text search in metadata, is tagging with keywords and the linking
of data using ontologies. However a keyword search can be very coarse as it may
provide access to a set of data but misses other essential and relevant data
tagged with close related keywords.  For example a keyword search on "weight"
of leaves will miss datasets tagged only with "dry weight" or "wet weight" that
might be of interest as well. The integration of semantic repositories that
provide taxonomies or ontologies can potentially improve the situation here.
These repositories can embed the keywords into a hierarchical or network
structure and so the query can be extended along known relations of the search
term.

Before data can effectively be reused it may needs to be cleaned, imputed,
reshaped and merged. This usually takes up to 70% of an analysis script (cite
Karin and me, and xxx). These preparatory steps are not only time and labour
intensive but also potentially error prone, especially if the amount and
complexity of data to be included increases. The integration of semantic
repositories that provide ontologies can help to solve these problems. As
ontologies allow the machine readable access to knowledge of a scientific
domain they can be used to model develop tools that "understand" the contents
of datasets and guide researchers on the process of data preparation. However
the development of ontologies especially for a research domain like ecology is
challenging. It is characterized by interdisciplinary interactions which leads
to a wide heterogeneous landscape of knowledge that would need to be covered
and formalized by the ontology.

Metadata as well as the concept of paper proposals can reduce the barrier to
data sharing and foster collaboration (cite Karin). While metadata allows an
insight into raw data without the need to give the data away, paper proposals
can serve as tool to discuss research ideas based on the metadata available.
The integration of semantic repositories potentially improves not only the
discovery of data but also assists researchers with the preparation of data on
reuse. A trending concept to streamline the processing of data is workflows.
They enable the access to data and metadata, the manipulation and analysis of
data as well as the preservation of valuable data products. The Kepler (cite
xxx) and the Pegasus (cite xxx) software are only two examples of software that
implement the workflow concept. However there is still demand on tools that
integrate a full set of data management concepts into widely accepted and
commonly used analysis software like R. 

We here introduce the `rbefdata` R package as companion to the open source data
management platform `BEFdata` (cite Karin). The package is part of the rOpenSci
(http://ropensci.org/) initiative which is a community driven project to
provide the R statistics environment (cite R) with a flexible access to
scientific data repositories. The R package enables access to data and metadata
stored on `BEFdata`, integrates semantic repositories stored on `tematres`
vocabulary servers (http://www.vocabularyserver.com/) and provides data
preservation functionality for raw research data as well as for free format
attachments files. We showcase the functionality of the `rbefdata` package
available with version 0.3.5. We create a workflow in form of an R script that
shows the semantic refinement of keywords to improve the dataset search, the
use of metadata, how to pull a complete set of data from a paper proposal into
the R environment, and finally the upload of data products. The workflow is
created along an analysis about N retention in the BEF-China experiment. The
results of the analysis have been published already and the data is open access
(Lang et al. 2013) which makes the workflow shown here simply reproducible. 

## Material and Methods 

### BEF-China 

The BEF (Biodiversity Ecosystem Functioning) - China project is a research
collaboration consisting of 10-15 independent research groups, whose
overarching aim is to disentangle the role of tree and shrub diversity for
production, erosion control, element cycling, and species conservation in
Chinese subtropical forest ecosystems. The BEF-China project (www.bef-china.de)
is funded by the German Science Foundation (DFG, FOR 891). It uses two main
research platforms located in the provinces Jiangxi and Zhejiang in China
(Bruelheide et al., 2012).  

### BEFdata platform

The [BEFdata](http://befdataproduction.biow.uni-leipzig.de/) platform is
specialized in the management of small and heterogeneous data. It offers data
harmonization features, adheres to standards like the Ecological Metadata
Language (EML) and fosters the exploration of data by keyword tagging.
Additionally the platform facilitates research cooperations by a paper proposal
tool. To create a paper proposal a researcher can select datasets on the
platform which are to be included in an analysis.  Furthermore basic
information like a title, a rationale, the envisaged journal and a date needs
to be provided. Submitting a proposal, a researcher asks for access to the data
and proposes his research idea to the project board and the data owners. 

The data owners get informed and can decide if and how they like to participate
in the upcoming analysis or if they only like to get acknowledged for providing
their data (cite Karin). This process allows to include or acknowledge all
researchers involved in the data sampling process, it promotes collaborations
between research units and helps to avoid duplication in publication
initiatives on the same research ideas which adds to the transparency of data
publication. Finally the datasets assembled in a paper proposal can be imported
in one step to the R environment by the `rbefdata` package. 

### The analysis: Nutrient retention along a biodiversity gradient

We use an analysis about N retention along biodiversity gradient in the
BEF-China experiment as a use case. We build a script based that shows the
functionalities and inter linkages between the BEF-China data platform and the
`rbefdata` package. The analysis is typical for interdisciplinary research in
ecology, as it combines soil, taxon, and nutrient data where data originating
from field campaigns of different collaborating laboratories has to be merged
prior to analyses. A paper proposal based on 3 datasets with the title "Mixed
afforestations of young subtropical trees promote nitrogen acquisition and
retention" has been created. The rationale given for the paper proposal is:

'Knowledge of biodiversity effects on nutrient cycling patterns in subtropical
forest ecosystems is still very limited, particularly as regards macro
nutrients such as nitrogen and phosphorus. Experimental approaches using tree
saplings may promote an understanding of mechanisms that underlie nutrient
acquisition and cycling in early successional stages of secondary forests and
forest plantations. Insights in the potential of nutrient retention of young
tree plantations are of particular interest in China, where large areas have
been reforested in order to counteract soil erosion and to increase the soils’
water and nutrient retention capacity. In this study we planted saplings of
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
(url). For a detailed description of the experimental design we refer to Lang
et al. 2013 

### Tematres 

The `tematres` vocabulary server can hold different representations of formal
knowledge like thesauri, taxonomies or ontologies. The `rbefdata` package
integrates the vocabulary of the BEF-China experiment stored on a `tematres`
server. It  provides relations of terms that can be used to improve the search
of relevant data for an analysis. The `befdata` packages uses the `rtematres` R
package to exploit the vocabulary server.

### rbefdata

`rbefdata` (GitHub: https://github.com/befdata/befdata) is the companion
package to the open source data management platform `BEFdata`. The latest
stable version of `rbefdata` can be installed via the CRAN package repository.
It is part of the rOpenSci initiative (http://ropensci.org/) which aims to
provide the R statistics environment with packages that enable access to
scientific data repositories. Basically the `rbefdata` package enables access
to data and the corresponding metadata stored on a `BEFdata` platform as well
as it allows the upload of data products. The integration of a `tematres`
vocabulary server allows for an improved exploration of datasets. By default it
integrates the `tematres` server but this can be changed by the package
options.

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
```

```
## Error: XML content does not seem to be XML:
## 'http://tematres.befdata.biow.uni-leipzig.de/vocab/services.php?task=fetchNotes&arg=74
## http://tematres.befdata.biow.uni-leipzig.de/vocab/services.php?task=fetchNotes&arg=534'
```

```r
term_info
```

```
## Error: object 'term_info' not found
```

```r

# get datasets tagged with plant organ
datasets_plant_organ = bef.get.datasets_for_keyword("plant organ")
datasets_plant_organ
```

```
##    id
## 1 357
## 2 202
## 3 187
##                                                                                                title
## 1                                              Biomass Allometry Equations of Pilot Experiment (SP7)
## 2 Carbon (C) and Nitrogen (N) Concentration (Root, Stem, Twig, Leaf) of 8 target species in the CSPs
## 3                                              Traits of ferns and herb species occuring in the CSPs
```

```r

# narrow down plant organ
narrow_tasks_plant_organ = bef.tematres.api(task = "fetchDown", "plant organ")
```

```
## Error: XML content does not seem to be XML:
## 'http://tematres.befdata.biow.uni-leipzig.de/vocab/services.php?task=fetchDown&arg=74
## http://tematres.befdata.biow.uni-leipzig.de/vocab/services.php?task=fetchDown&arg=534'
```

```r
narrow_tasks_plant_organ
```

```
## Error: object 'narrow_tasks_plant_organ' not found
```

```r

# enrich the search with narrower keywords
datasets_plant_organ_narrow = bef.get.datasets_for_keyword(c(narrow_tasks_plant_organ$term))
```

```
## Error: object 'narrow_tasks_plant_organ' not found
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


```r
# proposal id is
datasets = bef.get.datasets_for_proposal(id = 90)
extract_second_dataset = datasets[[2]]
head(extract_second_dataset, 5)
```

```
##     plot_id recov_plot perleaf_plot perroot_plot perbio_plot persoil_plot gbd_T0.mm.
## 1 pilot1D01     15.642        2.918       1.0015       3.920        96.08         NA
## 2 pilot1D02     13.032        5.523       1.3688       6.891        93.11      3.688
## 3 pilot1D04     20.292        1.057       0.5157       1.572        98.43      2.875
## 4 pilot1D05      9.595        4.187       1.0861       2.032        97.97      6.000
## 5 pilot1D07      8.354       15.100       5.0983      17.963        82.04      7.000
```

 
### Inspect data (EML)

Each dataset in the `BEFdata` platform is associated with metadata the authors
of the dataset provide. We also can access the metadata from within `rbefdata`.
It can be accessed either directly via a metadata download command that takes
the ID of a dataset or extracted from a dataset via the R internal
`attributes()` command. The extraction via attributes is possible as each
dataset is attached with its metadata when using one of the download commands
of `rbefdata` (see box below).


```r
# get metadata only, by dataset ID
bef.portal.get.metadata(dataset = 335)$title
```

```
## [1] "Competition of saplings for N -Pilot- system 15N retention"
```

```r

# extract title of first dataset in proposal
attributes(datasets[[1]])$title
```

```
## [1] "Competition of saplings for N -Pilot- 15N recovery in leaves and fine roots "
```

```r

# extract all dataset titles in the proposal
titles = sapply(datasets, function(x) attributes(x)$title)
titles
```

```
## [1] "Competition of saplings for N -Pilot- 15N recovery in leaves and fine roots "
## [2] "Competition of saplings for N -Pilot- system 15N retention"                  
## [3] "Plottreatment and -location within the blocks of the Pilot-Experiment"
```

```r

# other metadata available
names(attributes(datasets[[1]]))
```

```
##  [1] "names"                    "class"                    "row.names"               
##  [4] "title"                    "abstract"                 "publicationDate"         
##  [7] "language"                 "creators"                 "authors"                 
## [10] "intellectualRights"       "distribution"             "keywords"                
## [13] "generalTaxonomicCoverage" "samplingDescription"      "spatial_coverage"        
## [16] "temporal_coverage"        "related_material"         "columns"
```


The dataset list from the proposal contains three datasets, of which we do only
use the second and third. These two are written into two variables called
`Nretention` and `design` before deciding upon how to merge them. Inspecting
the headers of both dataset reveals each of them contains a column containing a
`plot_id` that seems suitable for merging. But we can also make use of the
metadata for the columns to check if this really is the case (see box below).


```r
# extract into separate datasets
Nretention = datasets[[2]]
design = datasets[[3]]

# overview about the contents of the datasets

# names in dataset Nretention
names(Nretention)
```

```
## [1] "plot_id"      "recov_plot"   "perleaf_plot" "perroot_plot" "perbio_plot"  "persoil_plot"
## [7] "gbd_T0.mm."
```

```r

# description of column plot_id
Nretention_column_plot_id_description = attributes(Nretention)$columns[1, ]$description
Nretention_column_plot_id_description
```

```
## [1] "Reasearch plots of the Biodiversity - Ecosystem functioning experiment (BEF-China). There are three main sites for research plots in the BEF Experiment: Comparative Study Plots (CSP) in the  Gutianshan Nature Reserve, having a size of 30x30m^2, measured on the ground. Main Experiment plots have a size of 1 mu, which is about 25x25m^2 in horizontal projection. Pilot Study Plots have a size of 1x1 m^2.  \nResearch plots on the main experiment have a \"p\" in front of their IDs and then a 6 digit code: Plots in the main sites A and B are named according to their position in the original spreadsheet, in which they were designed.  They consist of 6 digits: _1st digit_: Site (1:A, 2:B), _digit 2and3_: southwards row: as in spreadsheets the rows are named from the top to the bottom; _digit 4 and 5_: westward column: as in the original spreadsheet, but the letters are converted to numbers (A=01, B=02); _6th digit_: indicator, if the plot has been shifted a quarter mu.  Example: \"p205260\": \"p\" means that this is a plot that is specified.  \"2\" means, that we are at site B.  Now the coordinates of the south - west corner: \"0526\".  Since \"e\" is the fifth letter of the alphabet, this is Plot E26.   The last digit \"0\" means that this plot was not moved by a quarter of a Mu, as some sites in Site A. The 6th digit can also indicate the subplot within the plot. \"5\", \"6\", \"7\", \"8\" indicate the northwest, northeast, southeast, and southwest quarter plot respectively. (plot_id: plot_id; Datagroup description: Reasearch plots of the Biodiversity - Ecosystem functioning experiment (BEF-China). There are three main sites for research plots in the BEF Experiment: Comparative Study Plots (CSP) in the  Gutianshan Nature Reserve, having a size of 30x30m^2, measured on the ground. Main Experiment plots have a size of 1 mu, which is about 25x25m^2 in horizontal projection. Pilot Study Plots have a size of 1x1 m^2.  \nResearch plots on the main experiment have a \"p\" in front of their IDs and then a 6 digit code: Plots in the main sites A and B are named according to their position in the original spreadsheet, in which they were designed.  They consist of 6 digits: _1st digit_: Site (1:A, 2:B), _digit 2and3_: southwards row: as in spreadsheets the rows are named from the top to the bottom; _digit 4 and 5_: westward column: as in the original spreadsheet, but the letters are converted to numbers (A=01, B=02); _6th digit_: indicator, if the plot has been shifted a quarter mu.  Example: \"p205260\": \"p\" means that this is a plot that is specified.  \"2\" means, that we are at site B.  Now the coordinates of the south - west corner: \"0526\".  Since \"e\" is the fifth letter of the alphabet, this is Plot E26.   The last digit \"0\" means that this plot was not moved by a quarter of a Mu, as some sites in Site A. The 6th digit can also indicate the subplot within the plot. \"5\", \"6\", \"7\", \"8\" indicate the northwest, northeast, southeast, and southwest quarter plot respectively.)"
```

```r

# names in dataset Nretention
names(design)
```

```
##  [1] "block"                    "x"                        "y"                       
##  [4] "plot_id"                  "control_ID"               "block_community_code"    
##  [7] "community_number"         "species_mixture"          "species_diversity"       
## [10] "species_pool"             "species_code"             "research_group_colour"   
## [13] "control"                  "closed_canopy"            "density"                 
## [16] "Natives"                  "depth"                    "harvest"                 
## [19] "fungicide"                "inoculation"              "pesticide"               
## [22] "native"                   "genetic_diverstiy"        "seed_addition"           
## [25] "fertilizer"               "plot_treatment_connected" "sp1"                     
## [28] "sp2"                      "sp3"                      "sp4"                     
## [31] "sp5"                      "sp7"                      "sp8"                     
## [34] "sp11"                     "sp_connected"
```

```r

design_column_plot_id_description = attributes(design)$columns[4, ]$description
design_column_plot_id_description
```

```
## [1] "Reasearch plots of the Biodiversity - Ecosystem functioning experiment (BEF-China). There are three main sites for research plots in the BEF Experiment: Comparative Study Plots (CSP) in the  Gutianshan Nature Reserve, having a size of 30x30m^2, measured on the ground. Main Experiment plots have a size of 1 mu, which is about 25x25m^2 in horizontal projection. Pilot Study Plots have a size of 1x1 m^2.  \nResearch plots on the main experiment have a \"p\" in front of their IDs and then a 6 digit code: Plots in the main sites A and B are named according to their position in the original spreadsheet, in which they were designed.  They consist of 6 digits: _1st digit_: Site (1:A, 2:B), _digit 2and3_: southwards row: as in spreadsheets the rows are named from the top to the bottom; _digit 4 and 5_: westward column: as in the original spreadsheet, but the letters are converted to numbers (A=01, B=02); _6th digit_: indicator, if the plot has been shifted a quarter mu.  Example: \"p205260\": \"p\" means that this is a plot that is specified.  \"2\" means, that we are at site B.  Now the coordinates of the south - west corner: \"0526\".  Since \"e\" is the fifth letter of the alphabet, this is Plot E26.   The last digit \"0\" means that this plot was not moved by a quarter of a Mu, as some sites in Site A. The 6th digit can also indicate the subplot within the plot. \"5\", \"6\", \"7\", \"8\" indicate the northwest, northeast, southeast, and southwest quarter plot respectively. (plot_id: Individual complex ID for identifying exactly each plot; it connects with underline character the block number and the community code, i. e. the block number with the plots treatment. The plot identifier contains the information, which block the plot is in and which community is is comprised of.)"
```


### Analyse the data 

After merging the new synthesis dataset still contains many columns not
required for the analysis that can be dropped. To analyse the dataset of system
N retention we need information about the species diversity in the plots and
about which plot is placed in which block from the design dataset. 'Species
diversity' is used as a factor containing three levels (1,2,4 species
mixtures). The response variables have been checked for normality with `qqplot`
and transformed (see box below).


```r
# the synthesis dataset
syndata = merge(Nretention, design)

# overview about the content of the synthesis dataset
names(syndata)
```

```
##  [1] "plot_id"                  "recov_plot"               "perleaf_plot"            
##  [4] "perroot_plot"             "perbio_plot"              "persoil_plot"            
##  [7] "gbd_T0.mm."               "block"                    "x"                       
## [10] "y"                        "control_ID"               "block_community_code"    
## [13] "community_number"         "species_mixture"          "species_diversity"       
## [16] "species_pool"             "species_code"             "research_group_colour"   
## [19] "control"                  "closed_canopy"            "density"                 
## [22] "Natives"                  "depth"                    "harvest"                 
## [25] "fungicide"                "inoculation"              "pesticide"               
## [28] "native"                   "genetic_diverstiy"        "seed_addition"           
## [31] "fertilizer"               "plot_treatment_connected" "sp1"                     
## [34] "sp2"                      "sp3"                      "sp4"                     
## [37] "sp5"                      "sp7"                      "sp8"                     
## [40] "sp11"                     "sp_connected"
```

```r

# remove unwanted variables from synthesis datset
syndata = syndata[-c(9:14, 16:41)]
names(syndata)
```

```
## [1] "plot_id"           "recov_plot"        "perleaf_plot"      "perroot_plot"     
## [5] "perbio_plot"       "persoil_plot"      "gbd_T0.mm."        "block"            
## [9] "species_diversity"
```

```r

# > we want to use 'species_diversity' as a factor
syndata$species_diversity = as.factor(syndata$species_diversity)

# square root transforme response variables
syndata$recov_plot_t = syndata$recov_plot^0.5
syndata$perleaf_plot_t = syndata$perleaf_plot^0.5
syndata$perroot_plot_t = syndata$perroot_plot^0.5
syndata$persoil_plot_t = syndata$persoil_plot^0.5
```


We analysed our data by linear mixed effects models. Since the plots are nested
in blocks, we use block as a random factor. The analysis uses the R packages
`nlme` (Pinheiro et al. 2013) for modeling and `multcomp` (Hothorn et al. 2008)
for post-hoc comparisons. To adjust for an unbalanced experimental design an
ANOVA Type II was carried out to test for main effects using the R package
`car` (Fox and Weisberg 2011). The models have been evaluated visually.


```r
require(nlme)
require(multcomp)
require(car)
```



```r
### Model 1: Overall recovery/N retention
model1 = lme(recov_plot_t ~ gbd_T0.mm. + species_diversity, syndata, random = ~1 | block, na.action = na.omit, 
    method = "REML")
anova(model1)
```

```
##                   numDF denDF F-value p-value
## (Intercept)           1    34   870.6  <.0001
## gbd_T0.mm.            1    34     7.5  0.0098
## species_diversity     2    34     2.9  0.0714
```

```r
summary(glht(model1, linfct = mcp(species_diversity = "Tukey")))
```

```
## 
## 	 Simultaneous Tests for General Linear Hypotheses
## 
## Multiple Comparisons of Means: Tukey Contrasts
## 
## 
## Fit: lme.formula(fixed = recov_plot_t ~ gbd_T0.mm. + species_diversity, 
##     data = syndata, random = ~1 | block, method = "REML", na.action = na.omit)
## 
## Linear Hypotheses:
##            Estimate Std. Error z value Pr(>|z|)  
## 2 - 1 == 0   -0.378      0.251   -1.51    0.280  
## 4 - 1 == 0    0.478      0.420    1.14    0.482  
## 4 - 2 == 0    0.857      0.399    2.15    0.077 .
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## (Adjusted p values reported -- single-step method)
```

```r

# ANOVA type II test for unbalanced design
model1c = Anova(model1, type = "II")
model1c
```

```
## Analysis of Deviance Table (Type II tests)
## 
## Response: recov_plot_t
##                   Chisq Df Pr(>Chisq)   
## gbd_T0.mm.         7.42  1     0.0064 **
## species_diversity  5.71  2     0.0576 . 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

```r

### model evaluation checking plots to assess whether residuals are well behaved plot(model1)
### whether the response variable is a reasonable linear function of the fitted values
### plot(model1,recov_plot_t~fitted(.)) and whether the errors are reasonably close to normal
### distribution in all four blocks (Crawley 2009) qqnorm(model1,~resid(.)|block)

## Model2 percentage leaf recovery of plot recovery
model2 = lme(perleaf_plot_t ~ species_diversity, syndata, random = ~1 | block, method = "REML")
anova(model2)
```

```
##                   numDF denDF F-value p-value
## (Intercept)           1    36  273.06  <.0001
## species_diversity     2    36    6.56  0.0037
```

```r
summary(glht(model2, linfct = mcp(species_diversity = "Tukey")))
```

```
## 
## 	 Simultaneous Tests for General Linear Hypotheses
## 
## Multiple Comparisons of Means: Tukey Contrasts
## 
## 
## Fit: lme.formula(fixed = perleaf_plot_t ~ species_diversity, data = syndata, 
##     random = ~1 | block, method = "REML")
## 
## Linear Hypotheses:
##            Estimate Std. Error z value Pr(>|z|)    
## 2 - 1 == 0    1.053      0.293    3.59   <0.001 ***
## 4 - 1 == 0    0.865      0.497    1.74     0.18    
## 4 - 2 == 0   -0.188      0.479   -0.39     0.92    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## (Adjusted p values reported -- single-step method)
```

```r
Anova(model2, type = "II")
```

```
## Analysis of Deviance Table (Type II tests)
## 
## Response: perleaf_plot_t
##                   Chisq Df Pr(>Chisq)   
## species_diversity  13.1  2     0.0014 **
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

```r

# model evaluation plot(model2) plot(model2,recov_plot_t~fitted(.))
# qqnorm(model2,~resid(.)|block)

## Model3 percentage root recovery of overall recovery
model3 = lme(perroot_plot_t ~ species_diversity, syndata, random = ~1 | block, method = "REML")
anova(model3)
```

```
##                   numDF denDF F-value p-value
## (Intercept)           1    36   374.2  <.0001
## species_diversity     2    36     7.2  0.0024
```

```r
summary(glht(model3, linfct = mcp(species_diversity = "Tukey")))
```

```
## 
## 	 Simultaneous Tests for General Linear Hypotheses
## 
## Multiple Comparisons of Means: Tukey Contrasts
## 
## 
## Fit: lme.formula(fixed = perroot_plot_t ~ species_diversity, data = syndata, 
##     random = ~1 | block, method = "REML")
## 
## Linear Hypotheses:
##            Estimate Std. Error z value Pr(>|z|)   
## 2 - 1 == 0    0.601      0.170    3.53    0.001 **
## 4 - 1 == 0    0.733      0.288    2.54    0.028 * 
## 4 - 2 == 0    0.132      0.278    0.48    0.879   
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## (Adjusted p values reported -- single-step method)
```

```r
Anova(model3, type = "II")
```

```
## Analysis of Deviance Table (Type II tests)
## 
## Response: perroot_plot_t
##                   Chisq Df Pr(>Chisq)    
## species_diversity  14.3  2    0.00077 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

```r

# model evaluation plot(model3) plot(model3,recov_plot_t~fitted(.))
# qqnorm(model3,~resid(.)|block)

## Model 4 percentage soil recovery of overall recovery
model4 = lme(persoil_plot_t ~ species_diversity, syndata, random = ~1 | block, method = "REML")
anova(model4)
```

```
##                   numDF denDF F-value p-value
## (Intercept)           1    36   26248  <.0001
## species_diversity     2    36       4  0.0274
```

```r
summary(glht(model4, linfct = mcp(species_diversity = "Tukey")))
```

```
## 
## 	 Simultaneous Tests for General Linear Hypotheses
## 
## Multiple Comparisons of Means: Tukey Contrasts
## 
## 
## Fit: lme.formula(fixed = persoil_plot_t ~ species_diversity, data = syndata, 
##     random = ~1 | block, method = "REML")
## 
## Linear Hypotheses:
##            Estimate Std. Error z value Pr(>|z|)  
## 2 - 1 == 0   -0.294      0.127   -2.32     0.05 *
## 4 - 1 == 0   -0.499      0.215   -2.33     0.05 .
## 4 - 2 == 0   -0.205      0.207   -0.99     0.57  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## (Adjusted p values reported -- single-step method)
```

```r
Anova(model4, type = "II")
```

```
## Analysis of Deviance Table (Type II tests)
## 
## Response: persoil_plot_t
##                   Chisq Df Pr(>Chisq)  
## species_diversity  7.96  2      0.019 *
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

```r

# model evalution plot(model4) plot(model4,recov_plot_t~fitted(.))
# qqnorm(model4,~resid(.)|block)
```


### Results of the analysis

System 15N retention (overall plot recovery) was positively affected by species
richness at the level of P = 0.0576 (Chisq: 5.7; Fig. Xa). The analysis of the
different system compartments (leaves, fine roots and soil) revealed that fine
root recovery was lower than leaf recovery, and biomass recovery (leaves and
fine roots) was lower than soil recovery.  Whereas the relative leaf and root
recovery were significantly higher in species mixtures compared with
monocultures (Figs. Xb and Xc), the relative soil recovery was significantly
reduced (Fig. Xd). Thus, we could show that the relative N retention of biomass
was significantly increased in mixtures. For an interpretation of these
results we refer to Lang et al. 2013.

![plot of chunk anne_final_plot](figure/anne_final_plot.png) 


* caption:  Nitrogen (N) retention affected by species richness. N retention summed as
            the recovery of soil, roots and leaves (a), relative leaf recovery (b), relative root
            recovery (c) and relative soil recovery (d). Significant differences as revealed by post
            hoc Tukey’s test (P < 0.05) are indicated by different letters.

### Upload data 

Finally we need to decide on either to upload a full dataset which we could do
using the dataset upload function `bef.portal.upload.dataset()` or only to
upload the script and maybe a figure to highlight the road to the results from
the source datasets used. This can be done by attaching to the proposal with
the command `bef.portal.attach.to_proposal()`. For the example shown, it is the
best way to go with an attachment to the proposal as uploading the merged
dataset would only mean duplication of data in the database of the `BEFdata`
portal.

So we upload the script and the four pane figure with its caption to add them
to the proposal. The figure is prepared as Portable Network Graphics (PNG)
using the R internal PNG device. It is written to a temporary folder and then
uploaded. The script in this case is an R markdown file that we attach to the
proposal (see box below).


```r
# attach the script using a path
bef.portal.attach.to_proposal(id = 90, attachment = "./rbefdata.Rmd", description = "The R script that has been used to derive the results in the published paper")
```

```
## [1] "Attachment to proposal with ID: 90 successful!"
```



```
## pdf 
##   2
```



```r
# caption of the figure
caption = "Nitrogen (N) retention affected by species richness. N retention summed as\n           the recovery of soil, roots and leaves (a), relative leaf recovery (b), relative root\n           recovery (c) and relative soil recovery (d). Significant differences as revealed by post\n           hoc Tukey’s test (P < 0.05) are indicated by different letters."

# upload the figure
bef.portal.attach.to_proposal(id = 90, attachment = file.path(tempdir(), "results_plot_proposal_90.png"), 
    description = caption)
```

```
## [1] "Attachment to proposal with ID: 90 successful!"
```


![showcase_proposal_attachment](./figure/static/showcase_proposal_attachments.png)

* caption: The paper proposal in its final approved state with attachments. The
           attachments are the final results figure and the R script that has been 
           used to derive the results in the published paper.

## Discussion

There is a growing demand to use and reuse available data, which puts much
pressure on the development of software solutions that help researchers not
only to find but also to effectively reuse data (supporting). In ecology
especially the integration of small and heterogeneous data, which represent the
majority of datasets, seems promising as it potentially can be integrated into
a wider context to answer questions on a broader temporal and spatial scale
(cite xxx). However, particularly research areas like ecology which are
characterised by a high degree of interdisciplinary interactions are
challenging in terms of data management.

The software combination of `rbefdata` and `BEFdata` provides solutions to
different aspects of the data life cycle for ecological research groups. While
the `BEFdata` platform covers storage, and data harmonization tools, metadata
support and a social component that fosters sharing data online (cite Karin),
the `rbefdata` package gives easy access to data and metadata on the platform as
well as it provides upload functionality for datasets and attachments like
scripts or figures right from within R. Additionally, the tag based exploration
of datasets helps to find datasets relevant for a certain analysis. The
`tematres` vocabulary server integration further supports this as it allows to
retrieve term definitions as well as semantical relations to broaden or narrow
down search terms. 

`rbefdata` makes scripting a workflow to pull data for analysis and push back
results and scripts simple. The upload mechanism can help to keep the data
management platform up to date on the fly and gives other researchers the
possibility to reproduce results by downloading scripts attached. An uploaded
script is not only a stepping stone to reproducible research but also helps to
track down data provenance which can be interesting in acknowledging data
providers even for only one data column that has been used in an analysis. 

While it seems a waste of time and bandwidth on one hand to always transfer the
data to a local script for processing, this approach also has its upsides.
Having the data locally offers full flexibility in choice of tools and also
enables the researcher to freely mix in other local data sources. While this
approach works well for small data it does not for big data since the transfer
of data is not possible for large sized data. The recent trend here is
on-server/in-database statistics, a scenario where scripts are to be sent to
the server before it returns the answer after processing (xxx). To keep the
`BEFdata` platform as flexible as possible and to give the researchers the
freedom of choice this could be one of the future features to be integrated. 

### rbefdata makes metadata available within the R environment

.  `rbefdata` is innovative in that it
provides data together with metadata in the R environment.


### keeping workflow scripts close to the data: Provenance

While well described data helps a lot in understanding datasets and on
deciding upon the relevance and applicability of data for a certain analysis
there is still lots of manual intervention necessary to prepare the data for
analysis (cite Karin and me? or xxx). It may needs to be cleaned, imputed,
reshaped and merged which usually takes up to 70% of an analysis workflow,
before smart models can be applied to the data to find interesting patters
(cite the workflow paper of Karin and me). This preparatory steps not only are
time and labour intensive but also potentially error prone, especially as the
complexity of the analyses increases. Provenance and the advantage of keeping
scripts (workflows) close to the data.

Clarify: controlled vocabulary - thesaurus - ontology. Controlled vocabulary
for finding and sorting, ontology for automatic reasoning.

*** Semantics for searching and sorting

We decided not to develop functionality to develop nested controlled
vocabularies within BEFdata. This decision was based on the fact that there
are already sophisticated frameworks and software to develop and maintain
vocabularies. Linking to external vocabularies has the additional advantage
that several data repositories can simultaneously use the same thesaurus for
tagging their data. This keeps single repositories small and coherent without
loosing the potential to link them to other repositories (linked data,
citations for linked data).

*** Semantics for automated reasoning


This is a separate argument, and we do not touch it in the results: automatic
merging should be only in the discussion:

but also could be used in the process of integrating the data
for analysis. 

Additionally it can be error prone especially if analyses get more complex and
require the expertise of more than one research domain.  


Ontologies, as formal representations of knowledge, potentially offer a
sophisticated tool to deal with that step of data preparation (e.g michener et al 2012). 
While they are already used in some research domains like genetics (cite xxx, eg. http://www.geneontology.org/),
other domains face more problems using it (cite xxx, morpho team announced
semantic tagging but the plug-in did not appear anywhere). The application of
ontologies in ecology is discussed controversially (cite xxx) and it is argued
that they can be a huge benefit, but it is hard to set up a sophisticated
ontology covering all necessary terms and relation of a highly complex research
domain (cite xxx).


We recently started to develop an ontology using a `tematres` .The
formalization we develop will be based on the knowledge used in biodiversity
ecosystem functioning research. 

The `BEFdata` platform will get a semantical tagging feature that will allow data
owners to tag data fine granular ?? on data column level. Using the same
formalized knowledge from the ontology we will be able to provide smart merging
and transformation features within the `rbefdata` package that help researchers
to merge datasets semi automatic.

While data storage and description is almost the same for all kind of data the
effective interlinking of data via an ontology requires the development of a
common terminology. The terminology should not only be accepted but used, developped and discussed
by all contributing scientist of the project. The future goal on ontologies is of
course the development of domain ontologies that can be interlinked to an
overarching ontology. Thus, collaborative ontology
engineering approaches like `ontoverse` (Zoulfa El Jerroudi et al. 2008) or
`tematres` are highly valuable as they not only help to set up ontologies but
also to develop and maintain them over time even if the researchers change that
contribute to it.


## Acknowledgements

Thanks to all the data owners of the proposal for providing access to the
datasets. ...

## Literature

This will be done externally as markdown has no good way to deal with
references and stuff. We can collect here a list of links to references. I will
then collect them with e.g zotero to export a format we can hand them in for
publication.

## Appendix

### Figures

### saveaway 

We discuss `rbefdata` and `BEFdata` in in the light of current and future
challenges for data management give an outlook onto upcoming features that
could help to solve them. 

The data here is mainly provided by small scale studies spread all over the
world (e.g heidorn2009 shedding light on the dark) but also through bigger long
term projects like LTER (cite xxx), BEF-China (cite xxx), governmental projects
and local initiatives (cite xxx) and private persons. This in fact results in a
wild growing, complex and heterogeneous data landscape that an ontology would
need to capture to be usable.





### intro karin

Karin:

thesauri, ontologies, etc. ... 

Something on data discovery and paper
proposals: Interdisciplinary analyses depend on data coming from different
research fields. Not one single research project or laboratory measures all
data, but they come from different researchers.  Data discovery - finding data
that is suitable to answer a pressing question - has become an integral part of
science. Data discovery between scientific disciplines is hampered by different
vocabularies and missing agreement on common semantics. Tools addressing this
problem are



Introducing workflows, their merits, and ROpenSci. But also Kepler, Pegasus,
etc. Cite our paper on workflows.

 (http://ropensci.org/),
which is a community driven approach to wrap all science APIs and to create
solutions for R users to seamlessly pull data from different repositories
spread over the internet into R for analysis.  


### material and methods 

Karin: 
- I would suggest to reduce the details of the following dramatically:

The Main experiment was established in 2009 and 2010 as the first large scale
forest biodiversity–ecosystem functioning experiment in the highly species-rich
subtropics.  In total, the area covers 50 ha and there are 566 plots of 400
trees each, ranging in diversity from monoculture to 24-species mixtures. The
experiment used 42 native tree species and 10 shrub species, combined into
different species pools. More than 400 000 tree and shrub saplings were
planted.  In a parallel observational approach, a total of 27 Comparative Study
Plots (CSPs) of 30x30 m each were set up in existing forests in the adjacent
Gutianshan National Nature Reserve (Zhejiang Province) in 2008.  The
observational plots were selected according to a crossed sampling design along
tree species richness and stand age. The CSPs address the impact of
successional age on ecosystem functioning, providing a basis for assessing the
successional processes at work across tree species diversity in the Main
Experiment . 



### Data processing and integration

* sharing ideas for analysis: paper proposals 
      Paper proposals are an emerging concept solving transparant data exchange and
      reuse across disciplines and laboratories [citations!]


* Introducing workflows (merits, ROpenSci, Kepler, Pegasus, etc.) Cite our paper on workflows.
* Workflow repositories and software 
* R needs to be learned as well that is no argument to less acceptance of other tools like Kepler, is there?!
* Provenance and the advantage of keeping scripts (workflows) close to the data.


### Wrap up (introduce solutions)

Especially for highly interdisciplinary research domains this requires the
input of many scientists and discussions about definitions and relations of
terms in the representation.  This might be one of the reasons why there is a
lack of sophisticated ontologies especially for highly interdisciplinary
research domains like ecology. 




Karin: there are some papers talking about what users want from data
repositories. These could be cited (e.g. Kerstin Bach). Motivate that
researchers prefer to perform the analyses at their own laptops.


While data preservation and the access to data for a wider audience are covered
very well, the use of metadata and semantic concepts, which both are related to
the efficient reuse of data lacks behind.  On one hand this is related to the
reluctance of users to use new tools or the fear to loose control over valuable
data. But on the other hand this is also related to the fact that the valuable
concepts are not yet tightly integrated enough into the researchers daily
workflow.



* intro summary frame

A multitude of data management and knowledge platforms are emerging which
contribute to a growing global data pool. The need to effectively reuse the
available data, grows with the data pool. This puts much pressure on the
development of tools that tightly integrate valuable concepts into existing and
widely accepted tools and into the workflows of researchers to help them
dealing with the upcoming challenges in data management and analysis.

* data preservation -> many data available



