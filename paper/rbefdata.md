


## Abstract 

We face a deluge of data scientists need to deal with in many different
disciplines today. While there are already good solutions to some parts of the
data life cycle the applicability of the solutions to certain scientific
domains often varies. Especially research domains with high degree of
interdisciplinary interactions and heterogeneity in methods and data in general
like ecology face problems in dealing with some valuable concepts like
ontologies that potentially can be used to improve or automate some of the most
common tasks in analyses like finding relevant data, cleaning and merging of
datasets. We here introduce the `rbefata` package that connects to the open
source data management platform `BEFdata` that has been developed and is used
within the BEF-China experiment. We show the use of the package in combination
with the portal using an example workflow that integrates three datasets from
the BEF-China experiment representing an analysis that has been published
already.  We discuss the combination of the R package `rbefdata` and the data
portal in the context of state of the art data management as well as we give an
outlook on upcoming features that will bring semantical features like smart
merges based on an ontology we created. 

## Introduction 

With a growing awareness on value of data, much effort has been put into
building data management platforms, to preserve all kind of environmental and
historic data, over the last years (e.g. diversity workbench, `BEFdata`). Many
specialized solutions for different scientific disciplines appeared that
provide data management plans for small scale projects or collaborations as
well as for large data producing long term or remote sensing projects. An
ongoing trend in that context is the development of integrative databases or
data portals. They serve as nodes that collect data from smaller databases of a
certain domain and they give researchers of that domain the opportunity to
access a wide range of relevant data all from one place. These data management
portals in fact offer a solution to to one of the most pressing problems that
we face with our valuable data today, their lost. 

Another big problem, especially in terms of reuse of available data, is the
general understanding of datasets. Usually plain datasets say nothing, to one
who is not familiar with it and they are even hard to decipher by the author
itself after some time has passed. It is usually hard to remember exactly what
methods have been used to collect a certain columns data or what the
abbreviations or headers in the dataset mean. To solve this problem metadata
frameworks have been developed and published as standards so nobody really
needs to think about an own set of requirements to describe its data. The
Ecological Metadata Language is only one example for that. While this
theoretically solves the problem with not well described datasets it is still
hard to make people use it extensively as this usually always means to learn
new tools that help with the description process (e.g morpho, data up).

While well described data can help a lot in understanding datasets and on
deciding upon the relevance and applicability in a certain analysis there is
still lots of manual intervention necessary after that to prepare the data for
analysis (cite yourself and Karin? or xxx). It may needs to be cleaned,
imputed, reshaped and merged which usually takes up to 70% of an analysis
workflow, before the smart models can be applied to the data to find
interesting patters (cite the workflow paper of Karin and me). This preparation
steps not only are time and labour intensive but also potentially error prone,
especially as the complexity of analyses grows. 

Ontologies, formal representations of knowledge, potentially offer a
sophisticated tool to deal with that step of data preparation (cite supporting
ecology as data intensive science). While they are already used in some
research domains like genetics (cite xxx, eg. http://www.geneontology.org/),
other domains face more problems using it (cite xxx, morpho team announced
semantic tagging but the plug-in did not appear anywhere). For example in
ecology, that has grown into a very collaborative, interdisciplinary and data
intensive science over the last decade, to address questions on a greater
temporal and spatial scale (e.g michener et al 2012).  The data here is mainly
provided by small scale studies spread all over the world (e.g heidorn2009
shedding light on the dark) but also through bigger long term projects like
LTER (cite xxx), BEF-China (cite xxx), governmental projects and local
initiatives (cite xxx).  This in fact results in a wild growing, complex and
heterogeneous data landscape that we need to deal with. The application of
ontologies in ecology is thus discussed controversially (cite xxx) and it is
argued that they can be a benefit, but it is hard to set up a sophisticated
ontology covering all necessary terms and relation of a that complex research
domain like ecology (cite xxx).

With growing global data pool there is a growing demand to use and reuse
available data and to embed small heterogeneous data into a wider context. We
here introduce the R package `rbefdata` that in combination with the `BEFdata`
data management platform exactly deals with that. We showcase the functionality
of the package available with version 0.3.5 creating a workflow that integrates
two datasets using an analysis that has been published already and discuss the
`rbefdata` package and `BEFdata` in the light of upcoming developments like the
integration of an ontology we built that will make finding data and smart
merges possible, to help researchers to deal with the future challenges in
handling complex and heterogeneous data.

## Material and Methods 

### BEF-China and the BEFdata portal

The BEF-China experiment is a Biodiversity Ecosystem Functioning (BEF)
experiment funded by the German science foundation (DFG, FOR 891). It is
located in the subtropics of China in the provinces Jianxi and Zhejiang. The
BEF-China research group (www.bef-china.de) uses two main research platforms.
An experimental forest diversity gradient of 50~ha, and 27 observational plots
of 30x30 m each located in the Gutianshan Nature Reserve.  The observational
plots were selected according to a crossed sampling design along tree species
richness and stand age. The data for the workflow on carbon pools stems from 22
to 116 years consisting of 14 to 35 species (cite Bruelheide, 2010).  

The [BEFdata](http://befdataproduction.biow.uni-leipzig.de/) portal is an open
source data management platform developed within the BEF-China project. It
adheres to standards like the Ecological Metadata Language for describing
datasets with metadata and is specialized in harmonizing small heterogeneous
data that usually has to be dealt with in BEF. But its specialization makes it
also very valuable to use in any other scientific domain that needs to deal
with complex small and heterogeneous data. 

The portal offers a social component where researchers can shop datasets and
write a paper proposals based on the datasets in the shopping cart. In the
process of creating a proposal some information like a title, a rationale, an
envisaged journal and date needs to be provided. Sending in a proposal a
researcher asks for access to the datasets and provides the data owners with
necessary information about the paper. The data owners then can decide if and
how they like to participate in the upcoming paper or if they only like to get
acknowledged for providing their data (cite Karin).

### The proposal

We use an already published dataset as an example to present the
functionalities and inter linkages between the BEF-China data portal and
`rbefdata`. To test the effect of species richness on system N retention and
tree sapling N uptake we conducted a 15N tracer experiment in a young tree
plantation. To this end, saplings of four abundant early successional tree
species have been planted in monoculture, in two- and four-species mixtures,
and as individual trees. Afforestations are increasing globally to produce
timber and pulp wood, but also to enhance ecosystem services such as carbon
sequestration, nutrient retention, or groundwater recharge. In order to further
optimise these services with regard to balanced nutrient (particularly
nitrogen) cycles, it is important to know whether the use of mixtures of native
tree species in afforestation projects promotes greater acquisition and
retention of nitrogen compared to the currently established large-scale
monoculture. 

Four species were chosen for the experiment: Schima superba Gardn. et Champ.
and Elaeocarpus decipiens Hemsley (evergreen), Quercus serrata Murray and
Castanea henryi (Skan) Rehd. et Wils. (deciduous; Yu et al. 2001). The
following planting schemes were established in 1-mÂ² plots.  In each plot 16
saplings were planted in an array of four by four. Monocultures, two-species
combinations and four-species combinations were established. The four study
species provided a total of eleven species combinations four monocultures, six
two-species combinations, and one four-species combination. All treatments were
replicated four times, once in each of the four blocks. Pulse labelling with
15NH415NO3 (98% 15N) was performed in August and in September 2009. Leaf, fine
root and soil samples have been collected in September 2010. Samples have been
analysed for 15N content and leaf, fine root and soil recovery have been
calculated. The sum of the three compartment recoveries is referred to as
system N retention.  Relative leaf, root and soil recovery was calculated as
percentage of system N retention (for a detailed description of the material
and methods we refer to Lang et al. 2013). 


![showcase_proposal](./figure/static/showcase_proposal.png) 

* caption: The paper proposal in its final approved state. The information on that page contains a title 
          rational envisaged date and journal. The calculated authors and email lists for 
          communication as well as the attached datasets and sub projects involved (only partially shown).

### rbefdata 

The `rbefdata` package started its development within the BEF-Cina experiment.
Meanwhile it is part of the rOpenSci package portfolio (http://ropensci.org/),
which is a community driven approach to wrap all science APIs and to create
solutions to pull data from different repositories into R for analysis.  The
package can be installed from the CRAN package repository
(https://github.com/befdata/befdata) and enables access to the data, meta data
structures of the platform and provides convenient methods to pull single or
multiple dataset into the R environment in one step for analysis.  Additionally
it offers functions that help to upload final results datasets with the script
attached that has been used to derive the results from the original datasets
which provides a valuable insight into data provenance and also is a stepping
stone for reproducible research.

## Usecase (results)

The next step after an accepted paper proposal is to setup the `rbefdata`
package. This requires installing, loading the package and setting the required
package options. Having a look into the options list reveals several fields
that can be filled in, like the URL to the `BEFdata` server, user credentials
and a download folder name that is used to store free format files attached to
datasets. The `tematres` server related URLs in the options are part of
upcoming features that are non fully functional on the time of writing and thus
can be ignored by now. 

The most essential setting for the example workflow we present here is the user
credentials. These are used to authenticate the user against the portal to
ensure the access to the data has been granted before download and to log the
data access. Setting the server URL is not required here as it defaults to the
BEF-China project instance of the `BEFdata` portal that we retrieve data from
in this example. If one has set up an own instance of the `BEFdata` portal,
this URL needs to be changed so the package communicates with the right server
(see box below).


```r
require(rbefdata)
# options list
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

# querry single options
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





After setup we can start right away using data from the proposal that we
created. The proposal download function of `rbefdata` is used for that. It
draws all associated datasets of a proposal into the R environment in one
single step. It returns a list object that keeps a data frame per list element
containing a dataset of the proposal each (see blow). The function requires the
ID of the proposal to work. The ID can be found in the URL of the proposal (see
blow).

```
# the proposal URL shows the id is 90 
http://befdataproduction.biow.uni-leipzig.de/paperproposals/90
```


```r
# proposal id is
datasets = bef.get.datasets_for_proposal(id = 90)
extract_first_dataset = datasets[[1]]
head(extract_first_dataset, 5)
```

```
##     plot_id recov_plot perleaf_plot perroot_plot perbio_plot persoil_plot gbd_T0.mm.
## 1 pilot1D01     15.642        2.918       1.0015       3.920        96.08         NA
## 2 pilot1D02     13.032        5.523       1.3688       6.891        93.11      3.688
## 3 pilot1D04     20.292        1.057       0.5157       1.572        98.43      2.875
## 4 pilot1D05      9.595        4.187       1.0861       2.032        97.97      6.000
## 5 pilot1D07      8.354       15.100       5.0983      17.963        82.04      7.000
```


Each dataset in the `BEFdata` portal is associated with metadata the authors of
the dataset provide. We also provide access to the metadata from within
`rbefdata`. It can be accessed either directly via a metadata download command
that takes the ID of a dataset or extracted via the R internal `attributes()`
command. The extraction via attributes is possible as each dataset is attached
with its metadata when using one of the download commands of `rbefdata` (see
box below).


```r
# get metadtata only, by dataset ID
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
## [1] "Competition of saplings for N -Pilot- system 15N retention"
```

```r

# extract all dataset titles in the proposal
titles = sapply(datasets, function(x) attributes(x)$title)
titles
```

```
## [1] "Competition of saplings for N -Pilot- system 15N retention"           
## [2] "Plottreatment and -location within the blocks of the Pilot-Experiment"
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


The dataset from the proposal is written into two variables called `Nretention`
and `design` before deciding upon how to merge. Inspecting both dataset reveals
each of them contains a column with a `plot_id` that seems suitable for
merging. We also can use the metadata for columns to check if this really is
the case (see box below).


```r
# extract into separate datasets
Nretention = datasets[[1]]
design = datasets[[2]]

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

attributes(design)$columns
```

```
##                      header
## 1                     block
## 2                         x
## 3                         y
## 4                   plot_id
## 5                control_ID
## 6      block_community_code
## 7          community_number
## 8           species_mixture
## 9         species_diversity
## 10             species_pool
## 11             species_code
## 12    research_group_colour
## 13                  control
## 14            closed_canopy
## 15                  density
## 16                  Natives
## 17                    depth
## 18                  harvest
## 19                fungicide
## 20              inoculation
## 21                pesticide
## 22                   native
## 23        genetic_diverstiy
## 24            seed_addition
## 25               fertilizer
## 26 plot_treatment_connected
## 27                      sp1
## 28                      sp2
## 29                      sp3
## 30                      sp4
## 31                      sp5
## 32                      sp7
## 33                      sp8
## 34                     sp11
## 35             sp_connected
##                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         description
## 1                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   there are 4 blocks in the pilot experiment (block: block in the pilot-experiment the plot is belonging to, there are four main blocks (1-4) and four additional blocks (g1-g4) for analyzing the genetic diversity treatments )
## 2                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        Each of the 4 blocks was put in an x-y-diagram for locating each plot by its x- and y-value (x: the plots location in x-direction (1-13) within the block)
## 3                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        Each of the 4 blocks was put in an x-y-diagram for locating each plot by its x- and y-value (y: the plots location in y-direction (1-26) within the block)
## 4                                                                                                                                                                                                                                                                                                                                                Reasearch plots of the Biodiversity - Ecosystem functioning experiment (BEF-China). There are three main sites for research plots in the BEF Experiment: Comparative Study Plots (CSP) in the  Gutianshan Nature Reserve, having a size of 30x30m^2, measured on the ground. Main Experiment plots have a size of 1 mu, which is about 25x25m^2 in horizontal projection. Pilot Study Plots have a size of 1x1 m^2.  \nResearch plots on the main experiment have a "p" in front of their IDs and then a 6 digit code: Plots in the main sites A and B are named according to their position in the original spreadsheet, in which they were designed.  They consist of 6 digits: _1st digit_: Site (1:A, 2:B), _digit 2and3_: southwards row: as in spreadsheets the rows are named from the top to the bottom; _digit 4 and 5_: westward column: as in the original spreadsheet, but the letters are converted to numbers (A=01, B=02); _6th digit_: indicator, if the plot has been shifted a quarter mu.  Example: "p205260": "p" means that this is a plot that is specified.  "2" means, that we are at site B.  Now the coordinates of the south - west corner: "0526".  Since "e" is the fifth letter of the alphabet, this is Plot E26.   The last digit "0" means that this plot was not moved by a quarter of a Mu, as some sites in Site A. The 6th digit can also indicate the subplot within the plot. "5", "6", "7", "8" indicate the northwest, northeast, southeast, and southwest quarter plot respectively. (plot_id: Individual complex ID for identifying exactly each plot; it connects with underline character the block number and the community code, i. e. the block number with the plots treatment. The plot identifier contains the information, which block the plot is in and which community is is comprised of.)
## 5                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        Helper column to understand other columns in this data set (control_ID: character ID encoding the plots treatment in the narrower sense, e.g. fungicide- or pesticide-treatment; identical for each plot in one of the four blocks showing the same control ID.  The plot treatment in the experiment is coded as increasing caracters: A , B , C ,…, AA, AB, AC,…,AZ, BA)
## 6                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 The community code combines the plot tree community (as numbers) with the plot allocation to a subgroup (as letters) (block_community_code: The community code combines the plot tree community (as numbers) with the plot allocation to a subgroup (as letters))
## 7                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      Helper column to understand other columns in this data set (community_number: For representing the possible species combinations in an 4-species pool the species diversity is additional coded in increasing numbers: (1-4) = monocultural plots; (5-10) = 2-species plots; (11) = 4-species plots; (12) = 8-species plot.)
## 8                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Helper column to understand other columns in this data set (species_mixture: caracter scheme encoding the plots species diversity (1,2, 4 or 8 species per plot) by characters combinations; the characters number represents the plots species number and the character identity encodes the applied species pool within the pilot plot. For representing the possible species combinations in an 4-species (e.g. A,B,C,D for species pool 1) pool the species diversity is additional coded in caracter combinations: (A,B,C,D) = monocultural plots; (AB, AC, AD, BC, BD, CD) = 2-species plots; (ABCD) = 4-species plots; (AL) = 8-species plot.)
## 9                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 Taxon diversity can be given as species richness, or other diversity indices.  We also use rarefied species richness, shannon diversity index, and phylogenetic diversity indices. Rarefaction curves show the increase in species number with an increase of sampled individuals. R uses rarefy() from the package vegan to estimated species number for a given number of individuals. To compare different plots, the number of individuals should be smaller than the minimum number of individuals. -- The Shannon diversity is given by H = -sum (p_i log(p_i)), p_i is the relative abundance of the ith species. R provides this through the vegan package: diversity(x). -- The Simpson diversity is given by D = sum p_i^2, with p_i representing the relative abundance of the ith species. R provides this through the vegan package: diversity(x, index="simpson") -- Trees were counted when they exceeded 1m height. This data is aggregated from the raw data provided by Martin Böhnke and Martin Baruffol; in R with vegan: specnumber() -- Eveness as defined by Ricotta, C. A semantic taxonomy for diversity measures Acta Biotheoretica, 2007, 55, 23-33: shannon/log(rich) -- Phylogenetic diversity is calculated using Rao's Q. This is basically the mean distance of all pairswise distances between individuals in phylogenetic space. I used genus and family name to calculate phylogenetic distances between species. R provides Rao's Q and tools for calculating phylogenetic distances in the package ade4. Commands: as.taxo(), divc() (species_diversity: tree species diversity level within the pilot plot)
## 10                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               The plot design in pilot experiment was arranged with three different tree species pools containing four tree species.  (species_pool: The plot design in pilot experiment was arranged with three different tree species pools containing four tree species.\n\n)
## 11                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            2-character abbreviation encoding the species name and epithet of the tree species located within the plot (species_code: 2-character abbreviation encoding the species name and epithet of the tree species located within the plot)
## 12                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           plot colour used in the pilot experiment plot plan for representing the plots treatment applied to the different species pools (research_group_colour: plot colour used in the pilot experiment plot plan for representing the plots treatment applied to the different species pools)
## 13                                                                               _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (control: plot is used as control plot and is therefore not treated in any way)
## 14                                                                    _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (closed_canopy: plot is treated with a shading construction for imitating a closed canopy)
## 15                                                                               _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (density: density treatment with less or more than the 16 individuals per plot)
## 16                                                                                                                                            _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (Natives: Natives)
## 17                                                                                                                                                _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (depth: depth)
## 18                                                                                                                                            _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (harvest: harvest)
## 19                                                                                                       _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (fungicide: plot is treated with or without fungicides)
## 20                                                                                                    _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (inoculation: plot is treated with or without inoculation)
## 21                                                                                                       _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (pesticide: plot is treated with or without pesticides)
## 22 _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (native: the plots herb layer is treated either without or with seed addition of native herbs, non-native (=exotic) herbs or of a native-exotic herb mixture)
## 23                                              _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (genetic_diverstiy: plot is treated with seeds showing low, medium or high genetic diversity within the species)
## 24                                                                                       _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (seed_addition: plot is treated with (s) or without seed addition (ns))
## 25                                                                                                      _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (fertilizer: plot is treated with or without fertilizer)
## 26                                                   _control treatment_: For comparing and evaluating the influence of the different plot treatments on the biodiversity traits and developments some plots were used as control plots and were therefore not treated in any way. --- _simulating a closed tree canopy_: Some plots in the pilot experiment were treated with shading constructions for simulating a closed canopy. --- _density treatment_: For evaluating the impact of the individual density some plots were treated with more or less than 16 tree individuals per plot. --- _invasion treatment_: native and non native herb species were added to the plot. --- _depth treatment_: species were harvested at different soil depths --- _Fungicide treatment_: Plots in pilot experiment were treated with or without fungicides. --- _inoculation treatment_: some plots were treated with fungi inoculum. --- _pesticide treatment_: Plots in pilot experiment were treated with or without pesticides. --- _Differentiation between native, non-native and mixed (native + non-native) herb species that were established or added to the plots._: In some plots the focus was put on the herb layer whereby some were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Genetic diversity treatment_: The genetic diversity plots are located in additional blocks. On these plots the trees were apllied as seeds of low, medium or high genetic diversity instead of seedlings. --- _Seed addition treatment_: Some plots were treated with seed addition of native herbs, non-native herbs or a mixture of both. --- _Fertilizer treatment_: Some plots were treated with fertilizer of different concentrations --- _abbrevation code of all the treatments done on the plot_: For displaying the applied treatments done in the focused plot the treaments were not just coded as caracters but also as abbreviation code whereby each abbrevation is connected to one special treatment e.g. cc = closed canopy. (plot_treatment_connected: summarization of the plot treatments by connecting the treatments abbreviations)
## 27                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Research project within BEF China (sp1: plot is treated and analyzed by sp1)
## 28                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Research project within BEF China (sp2: plot is treated and analyzed by sp2)
## 29                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Research project within BEF China (sp3: plot is treated and analyzed by sp3)
## 30                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Research project within BEF China (sp4: plot is treated and analyzed by sp4)
## 31                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Research project within BEF China (sp5: plot is treated and analyzed by sp5)
## 32                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Research project within BEF China (sp7: plot is treated and analyzed by sp7)
## 33                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     Research project within BEF China (sp8: plot is treated and analyzed by sp8)
## 34                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   Research project within BEF China (sp11: plot is treated and analyzed by sp11)
## 35                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    Helper column to understand other columns in this data set (sp_connected: connecting the research project acronyms from the previous columns)
##             unit numericDomain
## 1           <NA>          <NA>
## 2  dimensionless          real
## 3  dimensionless          real
## 4           <NA>          <NA>
## 5           <NA>          <NA>
## 6           <NA>          <NA>
## 7           <NA>          <NA>
## 8           <NA>          <NA>
## 9  dimensionless          real
## 10          <NA>          <NA>
## 11          <NA>          <NA>
## 12          <NA>          <NA>
## 13          <NA>          <NA>
## 14          <NA>          <NA>
## 15          <NA>          <NA>
## 16          <NA>          <NA>
## 17          <NA>          <NA>
## 18          <NA>          <NA>
## 19          <NA>          <NA>
## 20          <NA>          <NA>
## 21          <NA>          <NA>
## 22          <NA>          <NA>
## 23          <NA>          <NA>
## 24          <NA>          <NA>
## 25          <NA>          <NA>
## 26          <NA>          <NA>
## 27          <NA>          <NA>
## 28          <NA>          <NA>
## 29          <NA>          <NA>
## 30          <NA>          <NA>
## 31          <NA>          <NA>
## 32          <NA>          <NA>
## 33          <NA>          <NA>
## 34          <NA>          <NA>
## 35          <NA>          <NA>
##                                                                                         info
## 1                                  Block code in the pilot experiment (block), dimensionless
## 2                         Within Block plot location in the pilot experiment. (x), numerical
## 3                         Within Block plot location in the pilot experiment. (y), numerical
## 4                                            BEF research plot name (plot_id), dimensionless
## 5                                                         Helper (control_ID), dimensionless
## 6  Within Block community code of the Pilot experiment (block_community_code), dimensionless
## 7                                                   Helper (community_number), dimensionless
## 8                                                    Helper (species_mixture), dimensionless
## 9                                  Taxonomic biodiversity (species_diversity), dimensionless
## 10                                     Species pool in the pilot experiment (species_pool), 
## 11              Species community code in the pilot experiment (species_code), dimensionless
## 12     Research group colour for the pilot experiment (research_group_colour), dimensionless
## 13                                  Treatment in the Pilot Experiment. (control), categories
## 14                            Treatment in the Pilot Experiment. (closed_canopy), categories
## 15                                       Treatment in the Pilot Experiment. (density), count
## 16                                  Treatment in the Pilot Experiment. (Natives), categories
## 17                                    Treatment in the Pilot Experiment. (depth), categories
## 18                                  Treatment in the Pilot Experiment. (harvest), categories
## 19                                Treatment in the Pilot Experiment. (fungicide), categories
## 20                              Treatment in the Pilot Experiment. (inoculation), categories
## 21                                Treatment in the Pilot Experiment. (pesticide), categories
## 22                                   Treatment in the Pilot Experiment. (native), categories
## 23                        Treatment in the Pilot Experiment. (genetic_diverstiy), categories
## 24                            Treatment in the Pilot Experiment. (seed_addition), categories
## 25                               Treatment in the Pilot Experiment. (fertilizer), categories
## 26                 Treatment in the Pilot Experiment. (plot_treatment_connected), categories
## 27                                       Research project within BEF China (sp1), categories
## 28                                       Research project within BEF China (sp2), categories
## 29                                       Research project within BEF China (sp3), categories
## 30                                       Research project within BEF China (sp4), categories
## 31                                       Research project within BEF China (sp5), categories
## 32                                       Research project within BEF China (sp7), categories
## 33                                       Research project within BEF China (sp8), categories
## 34                                      Research project within BEF China (sp11), categories
## 35                                                      Helper (sp_connected), dimensionless
```

```r
design_column_plot_id_description = attributes(design)$columns[4, ]$description
design_column_plot_id_description
```

```
## [1] "Reasearch plots of the Biodiversity - Ecosystem functioning experiment (BEF-China). There are three main sites for research plots in the BEF Experiment: Comparative Study Plots (CSP) in the  Gutianshan Nature Reserve, having a size of 30x30m^2, measured on the ground. Main Experiment plots have a size of 1 mu, which is about 25x25m^2 in horizontal projection. Pilot Study Plots have a size of 1x1 m^2.  \nResearch plots on the main experiment have a \"p\" in front of their IDs and then a 6 digit code: Plots in the main sites A and B are named according to their position in the original spreadsheet, in which they were designed.  They consist of 6 digits: _1st digit_: Site (1:A, 2:B), _digit 2and3_: southwards row: as in spreadsheets the rows are named from the top to the bottom; _digit 4 and 5_: westward column: as in the original spreadsheet, but the letters are converted to numbers (A=01, B=02); _6th digit_: indicator, if the plot has been shifted a quarter mu.  Example: \"p205260\": \"p\" means that this is a plot that is specified.  \"2\" means, that we are at site B.  Now the coordinates of the south - west corner: \"0526\".  Since \"e\" is the fifth letter of the alphabet, this is Plot E26.   The last digit \"0\" means that this plot was not moved by a quarter of a Mu, as some sites in Site A. The 6th digit can also indicate the subplot within the plot. \"5\", \"6\", \"7\", \"8\" indicate the northwest, northeast, southeast, and southwest quarter plot respectively. (plot_id: Individual complex ID for identifying exactly each plot; it connects with underline character the block number and the community code, i. e. the block number with the plots treatment. The plot identifier contains the information, which block the plot is in and which community is is comprised of.)"
```


After merging the datasets the new synthesis dataset still contains many column
not required for the analysis that have been dropped. To analyse the dataset of
system N retention we require the information about species diversity in the
plots and the information about which plot is placed in which block from the
design dataset.  

* some more glue text that describes what happens ... Anne???

The response variables have been checked for normality with `qqplot` and
transformed where necessary (box below).


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

# check for data properties (keep this?)
str(syndata)
```

```
## 'data.frame':	42 obs. of  9 variables:
##  $ plot_id          : Factor w/ 42 levels "pilot1D01","pilot1D02",..: 1 2 3 4 5 6 7 8 9 10 ...
##  $ recov_plot       : num  15.64 13.03 20.29 9.6 8.35 ...
##  $ perleaf_plot     : num  2.92 5.52 1.06 4.19 15.1 ...
##  $ perroot_plot     : num  1.001 1.369 0.516 1.086 5.098 ...
##  $ perbio_plot      : num  3.92 6.89 1.57 2.03 17.96 ...
##  $ persoil_plot     : num  96.1 93.1 98.4 98 82 ...
##  $ gbd_T0.mm.       : num  NA 3.69 2.88 6 7 ...
##  $ block            : Factor w/ 8 levels "1","2","3","4",..: 1 1 1 1 1 1 1 1 1 2 ...
##  $ species_diversity: int  1 1 1 2 2 2 2 2 4 1 ...
```

```r

# > we want to use 'species_diversity' as a factor
syndata$species_diversity = as.factor(syndata$species_diversity)

# square root transforme response variables
syndata$perroot_plot_t = syndata$perroot_plot^0.5
syndata$persoil_plot_t = syndata$persoil_plot^0.5
syndata$recov_plot_t = syndata$recov_plot^0.5
syndata$perleaf_plot_t = syndata$perleaf_plot^0.5
```


We analysed our data by linear mixed effects models. Since the plots are
clumped in space, we use block as a random factor. The analysis uses the R
packages `nlme` for modeling and `multcomp` for post-hoc comparisons. To adjust
for an unbalanced experimental design an ANOVA Type II was carried out to test
for main effects using the R package `car` (Fox & Weisberg 2011)  


```r
require(nlme)
require(multcomp)
require(car)
```



```r
### Model one Overall recovery/N retention
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

# model evaluation plot(model1,resid(.)~fitted(.)) plot(model1,recov_plot_t~fitted(.))

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

# model evaluation plot(model2,resid(.)~fitted(.)) plot(model2,perleaf_plot_t~fitted(.))

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
## 2 - 1 == 0    0.601      0.170    3.53   0.0012 **
## 4 - 1 == 0    0.733      0.288    2.54   0.0280 * 
## 4 - 2 == 0    0.132      0.278    0.48   0.8792   
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

# model evaluation plot(model3,resid(.)~fitted(.)) plot(model3,perleaf_plot_t~fitted(.))

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
## 2 - 1 == 0   -0.294      0.127   -2.32    0.050 .
## 4 - 1 == 0   -0.499      0.215   -2.33    0.049 *
## 4 - 2 == 0   -0.205      0.207   -0.99    0.573  
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

# model evalution plot(model4,resid(.)~fitted(.)) plot(model4,perleaf_plot_t~fitted(.))
```


System 15N retention (overall plot recovery) was positively affected by species
richness at the level of P = 0.l0576 (Chisq: 5.7; Fig. Xa). The analysis of the
different system compartments (leaves, fine roots and soil) revealed that fine
root recovery was lower than leaf recovery, and biomass recovery (leaves and
fine roots) was lower than soil recovery.  Whereas the relative leaf and root
recovery were significantly higher in species mixtures compared with
monocultures (Figs. Xb and Xc), the relative soil recovery was significantly
reduced (Fig. Xd).  Our results demonstrate that species richness of mixtures
increases system N retention in young subtropical tree plantations. Although
relative soil recovery was highest compared with relative leaf and root
recovery, soil recovery decreased with species richness (Fig. X). Thus, the
observed positive relationship between species richness and system N retention
is caused by an increase in relative N recovery of sapling biomass (fine roots
and leaves) with higher species numbers in mixtures. Our findings suggest
positive species diversity effects for an important ecosystem service, which is
highly relevant for afforestation programmes as currently applied in China on a
large scale. The positive relationship between species richness and system N
retention suggests that mixed plantings even at the sapling stage of a
restricted species pool may considerably increase N retention in subtropical
forest systems even after a few years. This in turn has the potential to
significantly reduce N losses and thus N accumulation in the leachate or
groundwater (Lang et al. 2013).

![plot of chunk anne_final_plot](figure/anne_final_plot.png) 


* caption:  Nitrogen (N) retention affected by species richness. N retention summed as
            the recovery of soil, roots and leaves (a), relative leaf recovery (b), relative root
            recovery (c) and relative soil recovery (d). Significant differences as revealed by post
            hoc Tukey’s test (P < 0.05) are indicated by different letters.


## Discussion

* General discussion 
  - high need to effective use/reuse data 
  - relevant data needs to be simply detectable 

* `BEFdata` and `rbefdata` 
  - in combination provide a solution to 
    + data storage
    + describing data with metadata
    + collaboration and data sharing 
    + simply pull data into analysis software and push data back
    + data provenance by attaching R scripts to uploads
  - will provide solution with next versions 
    + easier finding relevant data 
    + smart merges (including unit conversions)

As there is a growing demand to effectively reuse available data this puts much
pressure on the development of solutions that help researchers not only to find
but also to integrate heterogeneous small data into a wider context in
different analyses (cite xxx, data intensive science, long tail). The
combination of `BEFdata` and the `rbefdata` package provides a solutions to a
one part of the data life cycle and especially introduces a solution to deal
with high heterogeneous data.

We recently stared to develop an ontology using a `tematres` server containing
knowledge extracted from portals that deal with data management for ecological
research. The `tematres` server offers an API so all the contained terms can be
accessed by the upcoming version of `rbefdata` 

The formalization developed is and will be based on the knowledge used in
biodiversity research. Thus we will here discuss the software combination
`BEFdata` and `rbefdata` in the light of the upcoming features and in general
context state of the art data management today. In one of the next versions to
be rolled out the `BEFdata` portal will get a semantical annotation feature.
This will give administrators the ability to tag each column of datasets with a
general term that best describes the content. So the field will contain
potential top terms of the ontology. The tagging will be reflected in the API
and can thus be simply queried to use the information within the R package.
Using the knowledge about the content of a column in the R package will enable
us to do support smart merges that work.

`tematres` ([homepage](http://www.vocabularyserver.com/))into `BEFdata` and the
`rbefdata` package so they play well together semantically.

## Acknowledgements 

Thanks to all the data owners of the proposal for providing access to the
datasets. ...

## Literature

This will be done externally as markdown has no good way to deal with
references and stuff. We can collect here a list of links to references. I will
then collect them with e.g zotero to export a format we can hand them in for
publication.

## Appendix

* maybe will not be used extensively but we will see

### Figures 

* vizualization plugin (keywords) 

One can visualize the keywords associated with the dataset of a `BEFdata` portal
using the vitalization functionality. This gives a short overview about the
contents the portal data is dealing with.



```
## Warning: arbuscular mycorrhizal fungi could not be fit on page. It will not be plotted.
## Warning: chemical leaf composition could not be fit on page. It will not be plotted. Warning:
## competitive neighbourhood could not be fit on page. It will not be plotted. Warning:
## Gram-negative bacteria could not be fit on page. It will not be plotted. Warning:
## Gram-positive bacteria could not be fit on page. It will not be plotted. Warning: wood
## parenchym could not be fit on page. It will not be plotted. Warning: wood perforation plates
## could not be fit on page. It will not be plotted. Warning: air temperature could not be fit on
## page. It will not be plotted. Warning: base saturation could not be fit on page. It will not
## be plotted. Warning: biomass allocation could not be fit on page. It will not be plotted.
## Warning: cation exchange capacity could not be fit on page. It will not be plotted. Warning:
## data management could not be fit on page. It will not be plotted. Warning: digital data
## acquisition could not be fit on page. It will not be plotted. Warning: diversity treatment
## could not be fit on page. It will not be plotted. Warning: functional eveness could not be fit
## on page. It will not be plotted. Warning: intraspecific diversity could not be fit on page. It
## will not be plotted. Warning: leaf physical resistance could not be fit on page. It will not
## be plotted. Warning: phylogenetic diversity could not be fit on page. It will not be plotted.
## Warning: rarefied diversity could not be fit on page. It will not be plotted. Warning:
## secondary compounds could not be fit on page. It will not be plotted. Warning: spatial genetic
## structure could not be fit on page. It will not be plotted. Warning: trait dissimilarity could
## not be fit on page. It will not be plotted. Warning: tree rings could not be fit on page. It
## will not be plotted. Warning: wood compression could not be fit on page. It will not be
## plotted. Warning: wood shearing could not be fit on page. It will not be plotted. Warning:
## wood stretching could not be fit on page. It will not be plotted. Warning: wood toughness
## could not be fit on page. It will not be plotted. Warning: aboveground biomass could not be
## fit on page. It will not be plotted. Warning: basal area increment could not be fit on page.
## It will not be plotted. Warning: BEF China projects could not be fit on page. It will not be
## plotted. Warning: branch water potential could not be fit on page. It will not be plotted.
## Warning: cavity nesting hymenoptera could not be fit on page. It will not be plotted. Warning:
## climatic niche could not be fit on page. It will not be plotted. Warning: community similarity
## could not be fit on page. It will not be plotted. Warning: community weighted mean trait could
## not be fit on page. It will not be plotted. Warning: crown overlap could not be fit on page.
## It will not be plotted. Warning: crown projection area could not be fit on page. It will not
## be plotted. Warning: dbh distribution could not be fit on page. It will not be plotted.
## Warning: eco-physiologic traits could not be fit on page. It will not be plotted. Warning:
## experimental treatment could not be fit on page. It will not be plotted. Warning: Flora of
## China could not be fit on page. It will not be plotted. Warning: forest canopy could not be
## fit on page. It will not be plotted. Warning: genetic autocorrelation could not be fit on
## page. It will not be plotted. Warning: land use history could not be fit on page. It will not
## be plotted. Warning: litter biomass could not be fit on page. It will not be plotted. Warning:
## mineralisation could not be fit on page. It will not be plotted. Warning: mineralization could
## not be fit on page. It will not be plotted. Warning: multi-trophic interactions could not be
## fit on page. It will not be plotted. Warning: mycorrhiza could not be fit on page. It will not
## be plotted. Warning: nitrogen cycling could not be fit on page. It will not be plotted.
## Warning: non-random extinction could not be fit on page. It will not be plotted. Warning:
## parasitoids could not be fit on page. It will not be plotted. Warning: phylogenetic
## distinctness could not be fit on page. It will not be plotted. Warning: phytophagous insects
## could not be fit on page. It will not be plotted. Warning: PI meeting could not be fit on
## page. It will not be plotted. Warning: predators could not be fit on page. It will not be
## plotted. Warning: rainfall simulator could not be fit on page. It will not be plotted.
## Warning: research proposals could not be fit on page. It will not be plotted. Warning: rooting
## depth could not be fit on page. It will not be plotted. Warning: seedling could not be fit on
## page. It will not be plotted. Warning: slope form could not be fit on page. It will not be
## plotted. Warning: snag height could not be fit on page. It will not be plotted. Warning:
## social status could not be fit on page. It will not be plotted. Warning: specialization could
## not be fit on page. It will not be plotted. Warning: species identity variable could not be
## fit on page. It will not be plotted. Warning: temperature could not be fit on page. It will
## not be plotted. Warning: tree crown could not be fit on page. It will not be plotted. Warning:
## vegetation stratum could not be fit on page. It will not be plotted. Warning: Weibull
## distribution could not be fit on page. It will not be plotted. Warning: wood ground tissue
## could not be fit on page. It will not be plotted. Warning: wood mechanics could not be fit on
## page. It will not be plotted. Warning: wood porosity could not be fit on page. It will not be
## plotted.
```

![plot of chunk vizalize_keywords](figure/vizalize_keywords.png) 


### Tables
