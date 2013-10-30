


## Title

`rbefdata` - leveraging access to data and semantics

## Keywords 

Data management, data sharing, data processing, paper proposals, biodiversity ecosystem functioning, semantic integration
open source, open science 

## Abstract

A growing amount of data in ecology gets available which puts much pressure on
the development of tools that help researchers to deal with data exploration,
reuse, processing and the preservation of data products and their provenance.
Although many tools and concepts are available for data management not all of
them are widely spread throughout ecology due to different reasons. One of them
is a missing tight integration of valuable data management concepts into widely
used tools like the R environment for statistics. We designed an R package
named `rbefdata` that provides the R statistics environment with an access to
the open source data management platform `BEFdata` which is specialized in the
preservation and harmonization of small and heterogeneous ecological data. The
R package includes the access to the data stored on the platform as well as to
the metadata provided by dataset authors. The metadata can be accessed while
processing the data and thus gives a shortcut that helps in understanding the
associated data which facilitates the processing and analysis of data. The R
package integrates an online semantic repository (thesaurus) that can be used
to improve the search for datasets stored on the portal. Furthermore the R
package provides upload functionality so any data product can be pushed
directly back to the data portal for preservation. So we integrate data
management concepts like the semantic improved exploration of datasets, a
seamless access to data and metadata, for data processing and the preservation
of data products directly into the R environment. The open source character of
the data management platform `BEFdata` and the companion package `rbefata` make
it possible for any ecological project to used a sophisticate data management
solution with the benefit of closely integrated valuable concepts of data
management. 

## Introduction 

Today ecologists face a deluge of data which puts much pressure on the
development of tools that foster the exploration, the processing, the reuse and
the preservation of data. Although tools and concepts in data management
already provide many solutions to different parts of the life cycle of data,
not all of them are widely spread or accepted throughout ecology. This is
related to different reasons like the reluctance of researchers to use online
data management platforms or the lack of integration of data management
concepts into widely used software tools like for example the R statistics
environment. This situation can be improved by the tight integration of data
management concepts into existing and widely used software and thus into the
daily workflow of researchers. Paper proposals and data provenance as ways to
promote collaborations by the discussion of ideas and, metadata to improve data
preservation and information exchange as well as the integration of semantic
resources to enhance data exploration and processing, only represent a few
examples of concepts with the potential to improve the progress of a data
intensive scientific domain like ecology. The `rbefdata` R package in
combination with the data management platform `BEFdata` combine the strengths
of the data management concepts mentioned into a single and simple usable data
management package that makes use of widely accepted tools in ecology.

With a growing awareness on the value of data, many data management platforms
have been developed to preserve all kinds of environmental and historic data.
These provide data preservation plans for small scale projects as well as for
large scale, big data producing, long term or remote sensing collaborations
(cite e.g.  diversity workbench, `BEFdata`, DataONE, LifeWatch, Pangea, Bexis).
An ongoing trend in data preservation and accessibility is the development of
integrative data platforms (cite TRY, GBIF, Pangea). They serve as nodes that
collect data from smaller databases and enable researchers to access a wide
range of relevant data, all from one place. All these platforms offer a
solution to one of the most pressing problems in data management the loss of
valuable data (Heidorn, 2008). Even tough these platforms improve the situation
of data preservation, researchers are still reluctant to use online data
platforms as they fear to give away and loose the control over their data
(michener 2012). Here the `BEFdata` platform offers full control of uploaded
data via a fine grained access system. Uploading data from within R via the
`rbefdata` makes the data accessible to the owner only by default.

The demand to reuse available data grows with the amount of data available
(Heidorn, 2008). In ecology for example the reuse of data is of particular
interest as the integration of data offers the potential to answer questions on
a much broader temporal and spatial scale (michener, 2008). However a problem
with the reuse of data is, that available data is often not well described.
Metadata is necessary here as plain primary research data can be hard to
understand, and even hard to decipher by the authors themselves after some time
has passed. For example it is hard to remember what methods have been used to
collect the data of a certain column or what the abbreviations and the headers
in the dataset mean. However metadata is still not used exhaustive as it
usually always means to put more time into the collected data and to learn new
tools that help to describe it (e.g morpho, dataUP). Metadata gives researchers
the opportunity to describe their data and others to understand raw research
data even if they are not familiar with it (Fegraus 2005). Thus the `BEFdata`
portal sticks to the EML standard and the R package provides the metadata as
attributes of data frames right from within R.

To find relevant data for reuse is a challenging task that is getting even more
complex if more data gets available (Leinfelder et al, xxx). A common practice
in data discovery, next to full text search in data and metadata, is tagging
with keywords (Nadrowski 2013). However a keyword search can be very coarse as
it may provide access to a set of data but misses other essential and relevant
data tagged with close related or synonymous keywords (Leinfelder et al. xxx,
michener 2008). For example a keyword search on "weight" and "leaves" will miss
datasets tagged only with "dry weight", "wet weight" or "plant products" that
might be associated to datasets that are of interest as well. The integration
of semantic repositories that provide taxonomies can potentially improve the
situation here. These repositories can embed the keywords from the search query
into a hierarchical structure and so the query can be extended along known
relations of the search term (Leinfelder et al.). Thus the `rbefdata` package
enables the access to semantic repositories stored on `tematres` servers which
can be used with the keyword base dataset search of the `BEFdata` portal to
find relevant data.


and offers preservation for datasets and other data products like scripts and
figures that are generated while analysing data. We showcase the functionality
of the R package and the interactions with the data management platform using
an R script. It pulls and analyses data associated to a research idea in form
of a paper proposal from the `BEFdata` instance of the BEF-China experiment.
The analysis in the script deals with N retention along a biodiversity gradient
and asks for the influence of biodiversity on the process. The results of the
analysis have been published already and the data is open access. Thus the
analysis shown here to introduce the R package is fully reproducible by
executing the script.  We discuss the R package and the combination of software
in terms of the data life cycle and the current data management requirements in
ecology as well as we given an outlook on upcoming features of `rbefdata` and
`BEFdata`.


We here introduce the `rbefdata` R package as companion to the open source data
management platform `BEFdata` (Nadrowski 2013). The package is part of the
rOpenSci (http://ropensci.org/) initiative which is a community driven project
to provide the R statistics environment (R Development Core Team 2008) with a
flexible access to scientific data repositories. The R package enables access
to data and metadata stored on a `BEFdata` platform, integrates semantic
repositories stored on `tematres` vocabulary servers
(http://www.vocabularyserver.com/) and provides data preservation functionality
for raw research data as well as for free format attachments files that are
generated while analysing data with R. We showcase the functionality of the
`rbefdata` package available with version 0.3.5. The R script we present shows
the semantic refinement of keywords to improve the search of datasets, the use
of metadata in data processing, the access to a complete set of data based on a
paper proposal of the BEF-China experiment, and finally the upload of the data
products. The script contains an analysis about N retention that was done in
the BEF-China experiment. The results of the analysis have been published
already and the related data is open access (Lang et al. 2013). Thus the script
shown here is fully reproducible. 

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

The [BEFdata](http://befdataproduction.biow.uni-leipzig.de/) platform has been
developed as part of the BEF-China experiment. It is specialized in the
management of small and heterogeneous data that is typical for biodiversity
research. It offers data harmonization features, adheres to standards like the
Ecological Metadata Language (EML) for metadata support and fosters the
exploration of data by a keyword tagging and search system. The platform
facilitates research cooperations and the discussion of ideas by a paper
proposal tool. To create a paper proposal a researcher can select datasets on
the platform to be included in an analysis. Furthermore basic information like
a title, a rationale, the envisaged journal and a date needs to be provided.
Submitting a proposal, a researcher asks for access to the data and proposes
his research idea to the project board and the data owners.  The data owners
can decide if and how they like to participate in the upcoming analysis or if
they only like to get acknowledged for providing their data (Nadrowski 2013).
This process allows to include or acknowledge all researchers involved in the
data sampling process, it promotes collaborations between research units and
helps to avoid duplication in publication initiatives on the same research
ideas which adds to the transparency of data publication.  Finally all datasets
assembled in a paper proposal can be imported into the R environment by the
`rbefdata` package. 

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

The latest version of `rbefdata` can be installed from the CRAN repository by
the `install.packages()` command. After installation the package needs to be
loaded using the `require(rbefdata)` command. `rbefdata` offers a set of
options that modify the behavior of the R package. The options of the package
can be set or queried via the `bef.options()`. A look into the options list
(see box below) reveals several fields that can be filled in. One of the most
essential settings is the user credentials. These are used to authenticate the
user against the platform and to ensure weather the access to the specific
datasets has been granted or not. The credentials can be obtained from the
`BEFdata` platform where each user will find its credentials on its profile
page. The other options represent the URLs to the `BEFdata` server instance and
the `tematres` vocabulary server as well as a field that stores the name of a
download folder. While the URL fields ensure the package communicates with the
right servers the download folder name is used to create a folder in case we
download attached files from a dataset or proposal. The URL to `BEFdata` server
and the `tematres` defaults to the BEF-China project instances that we use to
retrieve data from. If an own instance of the `BEFdata` platform or `tematres`
has been set up, this URLs needs to be changed accordingly, so the package
communicates with the right server (see box below). As the data is open access
we need no authentication so we can stick to the default options. 


```r
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




* Caption: 
          The code box shows how to use the `bef.options()` command that is used to set
          and query the options of the `rbefdata` package which modify the behavior of
          the package. All options can ben shown at once to get anoverview as well as one
          can pick only a single one to display the value it is set to. The options can
          be set using the names of their fields shown here for the "user_credentials"
          and the "url".
  
### Data discovery 

The `rbefdata` package supports exploiting a `tematres` vocabulary server via
the `rtematres` package. We can find terms and relations as well as we can
display their descriptions in `rbefdata` which can be used to improve the
exploration of datasets. For example looking for datasets that deal with the
fresh weight of plant organs we are searching for the keywords "plant organs"
and "fresh weight". We can show the definition of the term "plant organs" first
if we like. We then ask the `BEFdata` platform for datasets that are tagged
with that terms and we get back a few datasets (see box xxx). 

In a next step we use the vocabulary on the `tematres` server to narrow down
"plant organs" and we find "leaf", "root", "twig" as well as plural forms. We
use the narrower keywords to query the `BEFdata` server again for datasets
associated with them and get back all datasets associated with the narrower
terms. This can be used the other way around as well to restrict the datasets
we get back to higher order terms with `bef.tematres.api(task = "fetchUp",
"plant organ")` (see box xxx).
 

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
datasets_plant_organ = bef.get.datasets.for_keyword("plant organ")
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
datasets_plant_organ_narrow = bef.get.datasets.for_keyword(c(narrow_tasks_plant_organ$term))
datasets_plant_organ_narrow
```

```
##     id
## 1  242
## 2  320
## 3  323
## 4  428
## 5  359
## 6  371
## 7  372
## 8  108
## 9  429
## 10 357
## 11 188
## 12 202
## 13 143
## 14 145
## 15 360
## 16 160
## 17 166
## 18 147
## 19 411
## 20 413
## 21 367
## 22 368
## 23 384
## 24 219
## 25 212
## 26 187
## 27 381
## 28 405
## 29 319
## 30 347
## 31 424
## 32 322
## 33 107
## 34 430
## 35 379
## 36 313
## 37 192
## 38 127
## 39 105
## 40 434
## 41 433
## 42 435
## 43 436
## 44 418
## 45 421
## 46 375
##                                                                                                                                            title
## 1                                                               Leaf traits and chemicals from 130 tree species in the Gutianshan Nature Reserve
## 2                                       Leaf traits and chemicals from 59 tree and shrub species in the main Experiment of BEF-China (Site A& B)
## 3                                                         Leaf traits and chemicals from individual trees in the Main Experiment (Sites A and B)
## 4                                                                                      Leaf traits and chemicals of 122 tree species in the CSPs
## 5                                                                                             Coarse root density in the Comparative Study Plots
## 6                                                                   Estimated Biomass of July 2010 of Pilot Experiment (SP7, Species Pool 1 & 3)
## 7                                                                                  Estimated Root Biomass of July 2010 of Pilot Experiment (SP1)
## 8                                   Talk 5: Leaf eco-physiological traits and coarse root spatial distribution characteristic in CSPs (2010)—SP3
## 9                                                                                    Tree - herb interactions and invasibility of exotic species
## 10                                                                                         Biomass Allometry Equations of Pilot Experiment (SP7)
## 11 Biomass of four tree species (Castanea henryi, Quercus serrata, Schima suberba and Elaeocarpus decipiens) as saplings in the Pilot Experiment
## 12                                            Carbon (C) and Nitrogen (N) Concentration (Root, Stem, Twig, Leaf) of 8 target species in the CSPs
## 13                                          Competition of tree saplings -Pilot- Biomass of target saplings - biomass allocation to constituents
## 14                                                Competition of tree saplings -Pilot- Biomass of target saplings - biomass allocation to strata
## 15                                                                                                                  Detailed tree allometry data
## 16                                                                                                          Genetic diversity of Ardisia crenata
## 17                                                                                                        Genetic diversity of Castanopsis eyrei
## 18                                                                         Herbivore damage on saplings of 23 tree and shrub species in the CSPs
## 19                                                                                        herbivory in the Main Experiment site A in summer 2009
## 20                                                                                                herbivory in the pilot experiment in fall 2010
## 21                                                                                              Leaf damage of tree individuals Site A fall 2011
## 22                                                                                            Leaf damage of tree individuals Site A summer 2011
## 23                                                                                                                          NILEX - Soil Erosion
## 24                                                                      Speficic leaf area (SLA) of Cunninghamia lanceolata and Pinus massoniana
## 25                                                              Leaf traits and chemicals from individual trees in the Gutianshan Nature Reserve
## 26                                                                                         Traits of ferns and herb species occuring in the CSPs
## 27                                                                           Tracer NILEx, decomposition rates of leaves and plot topograpy data
## 28                                                                                                 Leaf demography in the Main Experiment - 2011
## 29                                                                                                                  Site A tree census from 2010
## 30                                              Synthesis dataset: Plant traits aggregated from wood, leaf, and root traits of trees in the CSPs
## 31                                                                                                                    Cuttings experiment - CSPs
## 32                                                                         Leaf toughness from individual trees in the Gutianshan Nature Reserve
## 33                                           Talk 4: Constant functional diversity during secondary succession of a subtropical forest in Chinaf
## 34                                                                                        Functional traits herb layer community-main experiment
## 35                                                                           Functional traits of 45 species in subtropical forest in Dujiangyan
## 36                                                                                                    P concentrations in leaves and roots, CSPs
## 37                                                      Root Carbon (C) and Nitrogen (N) Concentration of 124 tree and shrub species in the CSPs
## 38                                                                                                CSP soil profile description II: soil horizons
## 39                                                                                       Talk 2: Research Progress for Belowground Biomass & NPP
## 40                                                                         Seed addition experiment  Site A (VIPs) – abiotic predictor variables
## 41                                                                                       Seed addition experiment  Site A (VIPs) - biomass data 
## 42                                                                                Seed addition experiment  Site A (VIP´s) – repeated monitoring
## 43                                                                                        Seed addition experiment  Site A (VIPs) – Tree heights
## 44                                                                                                                          Resident phytometers
## 45                                                                                            Pilot experiment: performance, biomass & herbivory
## 46                                          Functional traits of 14 subtropical woody species across a light-availability gradient in Dujiangyan
```


### Download data 

The `rbefdata` package leverages data access through paper proposals by a
download function. It loads all associated datasets of a proposal into the R
environment in one single step. It returns a list object that keeps a data
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
datasets = bef.get.datasets.for_proposal(id = 90)
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
of the dataset provide. We can also access the metadata from within `rbefdata`.
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
and transformed as shown in the box below.


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
require(car)
```



```r
### Model 1: Overall recovery/N retention
model1 = lme(recov_plot_t ~ gbd_T0.mm. + species_diversity, syndata, random = ~1 | block, na.action = na.omit, 
    method = "REML")
```

```
## Error: could not find function "lme"
```

```r
anova(model1)
```

```
## Error: object 'model1' not found
```

```r
summary(glht(model1, linfct = mcp(species_diversity = "Tukey")))
```

```
## Error: could not find function "glht"
```

```r

# ANOVA type II test for unbalanced design
model1c = Anova(model1, type = "II")
```

```
## Error: object 'model1' not found
```

```r
model1c
```

```
## Error: object 'model1c' not found
```

```r

### model evaluation checking plots to assess whether residuals are well behaved plot(model1)
### whether the response variable is a reasonable linear function of the fitted values
### plot(model1,recov_plot_t~fitted(.)) and whether the errors are reasonably close to normal
### distribution in all four blocks (Crawley 2009) qqnorm(model1,~resid(.)|block)

## Model2 percentage leaf recovery of plot recovery
model2 = lme(perleaf_plot_t ~ species_diversity, syndata, random = ~1 | block, method = "REML")
```

```
## Error: could not find function "lme"
```

```r
anova(model2)
```

```
## Error: object 'model2' not found
```

```r
summary(glht(model2, linfct = mcp(species_diversity = "Tukey")))
```

```
## Error: could not find function "glht"
```

```r
Anova(model2, type = "II")
```

```
## Error: object 'model2' not found
```

```r

# model evaluation plot(model2) plot(model2,recov_plot_t~fitted(.))
# qqnorm(model2,~resid(.)|block)

## Model3 percentage root recovery of overall recovery
model3 = lme(perroot_plot_t ~ species_diversity, syndata, random = ~1 | block, method = "REML")
```

```
## Error: could not find function "lme"
```

```r
anova(model3)
```

```
## Error: object 'model3' not found
```

```r
summary(glht(model3, linfct = mcp(species_diversity = "Tukey")))
```

```
## Error: could not find function "glht"
```

```r
Anova(model3, type = "II")
```

```
## Error: object 'model3' not found
```

```r

# model evaluation plot(model3) plot(model3,recov_plot_t~fitted(.))
# qqnorm(model3,~resid(.)|block)

## Model 4 percentage soil recovery of overall recovery
model4 = lme(persoil_plot_t ~ species_diversity, syndata, random = ~1 | block, method = "REML")
```

```
## Error: could not find function "lme"
```

```r
anova(model4)
```

```
## Error: object 'model4' not found
```

```r
summary(glht(model4, linfct = mcp(species_diversity = "Tukey")))
```

```
## Error: could not find function "glht"
```

```r
Anova(model4, type = "II")
```

```
## Error: object 'model4' not found
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
fine roots) was lower than soil recovery. Whereas the relative leaf and root
recovery were significantly higher in species mixtures compared with
monoculture (Figs. Xb and Xc), the relative soil recovery was significantly
reduced (Fig. Xd). Thus, we could show that the relative N retention of biomass
was significantly increased in mixtures. For an interpretation of these results
we refer to Lang et al. 2013.

![plot of chunk anne_final_plot](figure/anne_final_plot.png) 


* caption: Nitrogen (N) retention affected by species richness. N retention summed as the
           recovery of soil, roots and leaves (a), relative leaf recovery (b), relative
           root recovery (c) and relative soil recovery (d). Significant differences as
           revealed by post hoc Tukey’s test (P < 0.05) are indicated by different
           letters.

### Upload data 

Finally we need to decide on either to upload a full dataset which we could do
using the dataset upload function `bef.portal.upload.dataset()` or only to
upload the script and maybe a figure to highlight the road to the results from
the source datasets used. This can be done by attaching to the proposal with
the command `bef.portal.attach.to_proposal()`. For the example shown here, it
is the best way to go with an attachment to the proposal as uploading the
merged dataset would only mean duplication of data in the database of the
`BEFdata` portal.

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
## Error: specified file does not exist: /tmp/Rtmp2GkxZH/results_plot_proposal_90.png.  You must
## specify a valid file name or provide the contents to send.
```


![showcase_proposal_attachment](./figure/static/showcase_proposal_attachments.png)

* caption: The paper proposal in its final approved state with attachments. The
           attachments are the final results figure and the R script that has been 
           used to derive the results in the published paper.

## Discussion

* structure of intro
  * many data
  * reuse
  * metadata 
  * data search
  * preprocessing with semantics integrated
  * wrapup (metadata/paper proposals/workflows)

* potential structure of discussion?
  * Data life cycle 
  * Data preservation
  * Metadata 
  * Data exploration/processing
  * Metadata 
  * Semantics 
  * Taxonomies
  * BEFdata and rbefdata solutions

Even though the situation with data preservation has been improved by online
data management platforms, there is still many valuable data lost (long tail).
One one hand this is related to the fact that researchers are reluctant to use
online data management tools, as they fear to loose the control over their data
and on the other hand to the fact that most research projects do not have a
data preservation plan that would force the contributors to preserve their
data. More general this is related to no direct benefit to data providers for
sharing data online and that it usually only means to put more effort into the
data after the results have been published already. However the availability of
a broad range of data and useful metadata describing it is essential to
different aspects of the life cycle of data. In ecology the integration of
available data offers the potential to answer some of the most pressing global
relevant questions like for example about the global climate change and the
maintainability of vital ecosystem services. 

* BEFdata and rbefdata solutions
  * set incentives for data preservation
    * acknowledgement
    * contribution to upcoming papers 
    * data publishing (citable) 
  * use common tools transfer to metadata standards 
    * metadata from spreadsheets to EML  
  * reproducibility  
    * preservation of scripts as attachments to proposals/datasets

To further improve the situation on one hand is a strict policy related to
funding    

This requires efficient tools that not only help to access the data but also to
process it and to preserve data products and results including how they have
been derived to be fully reproducible as scripts or workflows

less effort has been put into preservation of algorithms and workflows that
researchers use to derive their data products and results.

The software combination `rbefdata` and `BEFdata` provides solutions to many of
these aspects of data management like data preservation, online data sharing
and discussion of ideas, data processing, intensive use of meta data and the
preservation of workflows used to derive results which is important for
reproducibility and provenance that in turn is again a crucial component to
provide effective incentives in form of acknowledgements for data providers.  
 
The `BEFdata` platform serves as a scratch pad for research data as well as it
covers the preservation of data. It offers data harmonization tools, metadata
support via the Ecological Metadata Language standard and a social component
that fosters sharing data online (cite Karin). The `rbefdata` package enables
access to the data and metadata on the platform as well as it provides upload
functionality right from within the R environment 

Lost a high amount of valuable data as researchers are still reluctant to give
away their data. One possible solution to this would be to make data
preservation obligatory and make it a condition for sponsorship of projects.


One one hand there is many
data already available. And on the other hand many data is still lost.

This requires the reuse and integration of mostly small and heterogeneous data.

Even though the situation gets better there is still many data lost as
researchers are reluctant to use online data preservation tools as they fear to
loose the control over their data.

Collaboration.


to preserve data products and
attachments that are generated on analysing data.  The tag based exploration of
datasets of the BEFdata platform improves the exploration of relevant data for
a certain analysis and the `tematres` vocabulary integration further supports
this. It allows to retrieve term definitions as well as relations to broaden or
narrow down search terms along a hierarchy. 

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



In ecology the reuse of the mostly small and heterogeneous data seems
promising. It can be integrated into a wider context to answer questions on a
much broader, temporal and spatial scale. 

This is of particular intrest in terms of the most pressing questions in
ecology

about climate changes and
ecosystem services. This requires several 

There is a growing demand to reuse available data and for tools that enable
researchers to deal with requirements like data preservation, exploration and
reuse as well as with the description process of data via meta data.  

 However, particularly research areas like ecology
which are characterised by a high degree of interdisciplinary interactions are
challenging in terms of data management and the applicability of some valuable
concepts like ontologies seems questionable. While ontologies with a very clear
and close scope are in use already (onto verse examples) the development of a
sophisticated ontology for ecology research is a very time, labor intensive and
complex task. The nature of ecology requires a community for the development of
ontologies that includes experts from all contributing domains to model the
relevant concepts into a formal representation.

(supporting, Kepler).






`rbefdata` makes scripting a workflow to pull data for analysis and push back
results and scripts simple. The upload mechanism can help to keep the data
management platform up to date and gives other researchers the possibility to
reproduce results by downloading scripts attached to proposals or datasets. An
uploaded script is not only a stepping stone to reproducible research but also
helps to track down data provenance which can be interesting in terms of
acknowledgement for data providers in a more fine grained view. 

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

`rbefdata` is innovative in that it
provides data together with metadata in the R environment.


### keeping workflow scripts close to the data: Provenance


Clarify: controlled vocabulary - thesaurus - ontology. Controlled vocabulary
for finding and sorting, ontology for automatic reasoning.

* Semantics for searching and sorting

We decided not to develop functionality to develop nested controlled
vocabularies within BEFdata. This decision was based on the fact that there
are already sophisticated frameworks and software to develop and maintain
vocabularies. Linking to external vocabularies has the additional advantage
that several data repositories can simultaneously use the same thesaurus for
tagging their data. This keeps single repositories small and coherent without
loosing the potential to link them to other repositories (linked data,
citations for linked data).

* Semantics for automated reasoning


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




Before data can effectively be reused it may need to be cleaned, imputed,
reshaped and merged which usually takes up to 70% of an analysis (Garijo 2012,
Pfaff 2013 in prep). These preparatory steps are not only time and labour
intensive but also potentially error prone, especially if the amount and
complexity of data to be included increases. The integration of ontologies can
help to solve these problems (michener 2008). As ontologies allow the machine
readable access to knowledge of a scientific domain they can be used to develop
tools that "understand" the contents of datasets and guide researchers on the
process of data preparation. While ontologies with a narrow and clear scope are
very well used already (cite xxx, e.g gene Ontology) it is a challenging tasks
to create an ontology for research domains like ecology that are characterized
by a high degree of interdisciplinary interactions (Parsons 2011). This
characteristic leads to a heterogeneous landscape of knowledge and concepts
that would need to be covered and formalized by the ontology.


As the `BEFdata` platform is open source each project can set up an own
instance profit from the data sharing and preservation offers data preservation
and harmonizing functionality.  The `rbefdata` package enables an easy access
to the data preservation from within R and the   




We discuss `rbefdata` and `BEFdata` in in the light of current and future
challenges for data management give an outlook onto upcoming features that
could help to solve them. 

The data here is mainly provided by small scale studies spread all over the
world (e.g heidorn2009 shedding light on the dark) but also through bigger long
term projects like LTER (cite xxx), BEF-China (cite xxx), governmental projects
and local initiatives (cite xxx) and private persons. This in fact results in a
wild growing, complex and heterogeneous data landscape that an ontology would
need to capture to be usable.


data management concepts into existing and widely
used software and thus into the daily workflow of researchers in ecology. Paper
proposals and data provenance as a way to promote the discussion of ideas and
collaborations, metadata to improve data preservation and information exchange
for data reuse as well as the integration of semantic resources to enhance data
exploration and its processing, only represent a few examples of concepts with
the potential to improve the progress of a data intensive scientific domain
like ecology. The `rbefdata` R package and the `BEFdata` platform are an
approach to combine the strengths of the mentioned data management concepts
into a single and simple usable data management package.




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



