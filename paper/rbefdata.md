


## Abstract

Today scientists need to deal with a deluge of data in many different
disciplines. While there are already good software solutions to assist
researcher throughout the data life cycle, the applicability of the solutions
to certain scientific domains often varies. We here introduce the R statistics
package `rbefata` that connects to the open source data management platform
`BEFdata` that has been developed and is used within the BEF-China experiment.
We show the use of the package and its interaction with the data management
platform using an example workflow that integrates two datasets from the
BEF-China experiment. The analysis in the workflow is representing already
published results, so the data will be open access in the near future. We
discuss the introduced combination of software in the context of the data life
cycle and current as well as future data management requirements.  Additionally
we give an outlook on upcoming semantical features like an assisted search and
smart merging functionality to be integrated with `rbefdata` and `BEFdata`.

## Introduction

With a growing awareness on the value of data, much effort has been put into
building data management platforms, to preserve all kind of environmental and
historic data, over the last years (e.g. diversity workbench, GBIF, `BEFdata`,
DataONE, LifeWatch). Many solutions for different scientific disciplines
appeared that provide data management plans for small scale projects or
collaborations as well as for large data producing, long term or remote sensing
projects. An ongoing trend in that context is the development of integrative
databases or data portals. They serve as nodes that collect data from smaller
databases of a certain domain and they give researchers of that domain the
opportunity to access a wide range of relevant data all from one place (e.g
GBIF, TRY). These data management portals in fact offer a solution to to one of
the most pressing problems that we face with our valuable data today, their
loss.

There is a growing demand to use and reuse this preserved data. By developing
tools that allow an easy access to the data for analyses, it can be assured
that it is, reused and embedded into into a wider context. A problem here is
the legibility of datasets. Usually plain datasets say nothing, to one who is
not familiar with it and they are even hard to decipher by the author himself
after some time has passed. It is hard to remember exactly what methods have
been used to collect a certain columns data or what the abbreviations or
headers in the dataset mean. 

Metadata frameworks have been developed and published as standards to solve
this problem, so nobody really needs to think about an own set of requirements
to describe his data. The Ecological Metadata Language
[EML](http://knb.ecoinformatics.org/software/eml/) is only one example for
that. While this theoretically solves the problem with not well described
datasets it is still hard to make researchers use it extensively as this
usually always means to learn new tools that help with the description process
(e.g morpho, data up).

In this paper we introduce the new R package `rbefdata` which links the R
statistics Environment to the open source data management platform `BEFdata`.
The `rbefdata` package is part of the rOpenSci initiative which aims to give
R-Users all the flexibility to access a wide range of data repositories. The
aim of the `rbefdata` package is to provide a tool which helps to download and
analyse data as well to provide upload functionality to push back new datasets,
scripts and figures to the data management portal. Additionally the package
offers methods that ease the exploration of datasets by the integration of a
vocabulary server. 

We showcase the functionality of the package available with version `0.3.5`
creating a workflow that integrates two datasets. The use case is dealing with
data from a small scale experiment called pilot experiment in the BEF-China
experiment. It is a 15N tracer experiment which aims to disentangle the effect
of species mixtures on system N retention. The workflow depicts how to pull
data into the R environment, the inspection of datasets metadata and how to
upload data and attachments. The analysis in the workflow reconstructs a facet
of an analysis that has been published already by Lang et al. 2013. 

## Material and Methods

### BEF-China 

The BEF- (Biodiversity and Ecosystem Functioning) China project is a research
group whose aim is to disentangle the 'The role of tree and shrub diversity for
production, erosion control, element cycling, and species conservation in
Chinese subtropical forest ecosystems'. The BEF-China research group
(www.bef-china.de) is funded by the German science foundation (DFG, FOR 891)
and uses two main research platforms located in the provinces Jiangxi and
Zhejiang.  The Main experiment was established in 2009 and 2010 as the first
large scale forest biodiversity–ecosystem functioning (BEF) experiment in the
highly species-rich subtropics.  In total, the area covers 50 ha and there are
566 plots of 400 trees each, ranging in diversity from monoculture to
24-species mixtures. The experiment used 42 native tree species and 10 shrub
species, combined into different species pools. More than 400 000 tree and
shrub saplings were planted.  In a parallel observational approach, a total of
27 Comparative Study Plots (CSPs) of 30x30 m each were set up in existing
forests in the adjacent Gutianshan National Nature Reserve (Zhejiang Province)
in 2008.  The observational plots were selected according to a crossed sampling
design along tree species richness and stand age. The CSPs address the impact
of successional age on ecosystem functioning, providing a basis for assessing
the successional processes at work across tree species diversity in the Main
Experiment (Bruelheide et al., 2012). 

### BEFdata portal

The [BEFdata](http://befdataproduction.biow.uni-leipzig.de/) is specialized in
managing small and heterogeneous datasets. It adheres to standards like EML and
offers a social component as well. The portal facilitates research cooperation
by the tool of paper proposals.  Sending in a proposal, a researcher asks for
access to the datasets and proposes his research idea to the data owners and
possible collaborators. This more social component of the portal allows to
include and acknowledge all researchers involved in the data sampling process,
promotes collaborations between research units, avoids publication initiatives
of the same research ideas and adds to the transparency of data publication.
To create a paper proposal the researcher can shop (select) datasets which are
to be included in the analyses.  Furthermore basic information of the proposed
paper such as the title, the rationale, the envisaged journal and date needs to
be provided. The data owners and proposed collaborators are informed and can
decide if and how they like to participate in the upcoming paper or if they
only like to get acknowledged for providing their data (cite Karin).
Furthermore the datasets assembled by the paper proposal can be readily
imported in one step to the R environment by `rbefdata`.

### The proposal

Starting on with a paper proposal on following rationale.  

We created a paper proposal with the following rationale: 'Knowledge of
biodiversity effects on nutrient cycling patterns in subtropical forest
ecosystems is still very limited, particularly as regards macro nutrients such
as nitrogen and phosphorus. Experimental approaches using tree saplings may
promote an understanding of mechanisms that underlie nutrient acquisition and
cycling in early successional stages of secondary forests and forest
plantations. Insights in the potential of nutrient retention of young tree
plantations are of particular interest in China, where large areas have been
reforested in order to counteract soil erosion and to increase the soils’ water
and nutrient retention capacity.  In this study we planted saplings of four
abundant early successional (evergreen and deciduous) tree species in
monoculture, two- and four-species combination to test the effect of species
richness on nitrogen acquisition and retention by using a 15N tracer
experiment. A crucial question in BEF research is the appropriate time scale of
experiments which allows species richness effects to emerge. This question
gains importance when long-lived and slowly growing organisms such as trees are
considered. We wanted to analyse whether species richness effects occur during
the establishment phase of early successional tree species typical of
subtropical forests of China.  More precisely we wanted to test the following
hypotheses: (H1) Nitrogen acquisition and retention increases with species
richness due complementary effects in species mixtures.  (H2) Species richness
effects strengthen over time.' The respective proposal can be assessed under
(url) For a detailed description of the experimental design we refer to Lang et
al. 2013 (DOI)

### rbefdata

The development of the `rbefdata` package started within the BEF-China project.
Meanwhile it is part of the rOpenSci package portfolio (http://ropensci.org/),
which is a community driven approach to wrap all science APIs and to create
solutions for R users to seamlessly pull data from different repositories
spread over the internet into R for analysis. The package can be installed from
the CRAN package repository (https://github.com/befdata/befdata) (see box
below). It enables access to the data and meta data structures of the platform
and provides convenient methods to pull single or multiple dataset into the R
environment in one step for analysis. Additionally it offers functions that
help to upload final results datasets with the script attached that has been
used to derive the results from the original datasets which provides a valuable
insight into data provenance and also is a stepping stone for reproducible
research.


```r
install.packages("rbefdata")
```


## Example workflow (results)

In this paper we use an already published analysis as a use case to build a
workflow that shows the functionalities and inter linkages between the
BEF-China data portal and the `rbefdata` package. We start setting up the R
package, highlight the dataset exploration features including the vocabulary
integration over a `tematres` server, before we finally come to the paper
proposal and the download of data as well as to the upload of final results.

After loading `rbefdata` into the working environment the settings need to be
set via the `bef.options()` command. Having a look into the options list we see
several fields that can be filled in. The most essential setting for the
example workflow we present here is the user credentials. These are used to
authenticate the user against the portal and to ensure the access to the data
has been granted as well as to log the data access. We need this as the data is
not yet open access. But it will be in the near future and then a key is no
longer required to download the data.

Other options we see here are the URLs to the `BEFdata` instance and the
`tematres` server as well as a field that stores the name of a download folder.
While the URL fields ensure the package communicates with the right servers the
download folder name is used to create a folder in case we download attached
files from a dataset or proposal. In our case there is no need to change the
URL to `BEFdata` as it defaults to the BEF-China instance that we use to
retrieve data from. If one has set up an own instance of the `BEFdata` portal,
this URL needs to be changed so the package connects to the right server (see
box below).


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





### Tematres vocabulary integration 

A `tematres` server can hold different representations of formalized knowledge
like a thesaurus or even an ontology of a project. The `rbefdata` package
supports exploiting a `tematres` vocabulary server via the `rtematres` package.
We can find terms and relations as well as we can display their descriptions in
`rbedfata`. This can be used to improve the exploration of datasets. For
example looking for datasets that deal with  "plant organs" we can display the
definition of that task first (box below). Then we ask the `BEFdata` portal for
datasets that are tagged with the keyword we are looking for. We get back a few
datasets. In a next step we use the vocabulary on the `tematres` server to
narrow down "plant organs" and we find "leaf",  "root", "twig" as well as
plural forms. We use the narrower keywords to query the `BEFdata` server again
for datasets associated with them.


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
## [1] "73" "75" "76" "30"
## 
## $term
## [1] "leaf"  "root"  "roots" "twig"
```

```r

# enrich the search with narrower keywords
datasets_plant_organ_narrow = bef.get.datasets_for_keyword(c(narrow_tasks_plant_organ$term))
datasets_plant_organ_narrow
```

```
##     id
## 1  242
## 2  320
## 3  323
## 4  359
## 5  371
## 6  372
## 7  108
## 8  357
## 9  188
## 10 202
## 11 143
## 12 145
## 13 360
## 14 160
## 15 166
## 16 147
## 17 367
## 18 368
## 19 384
## 20 219
## 21 212
## 22 187
## 23 381
## 24 319
## 25 347
## 26 322
## 27 107
## 28 192
## 29 313
## 30 105
##                                                                                                                                            title
## 1                                                               Leaf traits and chemicals from 130 tree species in the Gutianshan Nature Reserve
## 2                                       Leaf traits and chemicals from 59 tree and shrub species in the main Experiment of BEF-China (Site A& B)
## 3                                                         Leaf traits and chemicals from individual trees in the Main Experiment (Sites A and B)
## 4                                                                                             Coarse root density in the Comparative Study Plots
## 5                                                                   Estimated Biomass of July 2010 of Pilot Experiment (SP7, Species Pool 1 & 3)
## 6                                                                                  Estimated Root Biomass of July 2010 of Pilot Experiment (SP1)
## 7                                   Talk 5: Leaf eco-physiological traits and coarse root spatial distribution characteristic in CSPs (2010)—SP3
## 8                                                                                          Biomass Allometry Equations of Pilot Experiment (SP7)
## 9  Biomass of four tree species (Castanea henryi, Quercus serrata, Schima suberba and Elaeocarpus decipiens) as saplings in the Pilot Experiment
## 10                                            Carbon (C) and Nitrogen (N) Concentration (Root, Stem, Twig, Leaf) of 8 target species in the CSPs
## 11                                          Competition of tree saplings -Pilot- Biomass of target saplings - biomass allocation to constituents
## 12                                                Competition of tree saplings -Pilot- Biomass of target saplings - biomass allocation to strata
## 13                                                                                                                  Detailed tree allometry data
## 14                                                                                                          Genetic diversity of Ardisia crenata
## 15                                                                                                        Genetic diversity of Castanopsis eyrei
## 16                                                                         Herbivore damage on saplings of 23 tree and shrub species in the CSPs
## 17                                                                                              Leaf damage of tree individuals Site A fall 2011
## 18                                                                                            Leaf damage of tree individuals Site A summer 2011
## 19                                                                                                  NILEX - Rainfall Simulation and Soil Erosion
## 20                                                                      Speficic leaf area (SLA) of Cunninghamia lanceolata and Pinus massoniana
## 21                                                              Leaf traits and chemicals from individual trees in the Gutianshan Nature Reserve
## 22                                                                                         Traits of ferns and herb species occuring in the CSPs
## 23                                                                           Tracer NILEx, decomposition rates of leaves and plot topograpy data
## 24                                                                                                                  Site A tree census from 2010
## 25                                              Synthesis dataset: Plant traits aggregated from wood, leaf, and root traits of trees in the CSPs
## 26                                                                         Leaf toughness from individual trees in the Gutianshan Nature Reserve
## 27                                           Talk 4: Constant functional diversity during secondary succession of a subtropical forest in Chinaf
## 28                                                      Root Carbon (C) and Nitrogen (N) Concentration of 124 tree and shrub species in the CSPs
## 29                                                                                                    P concentrations in leaves and roots, CSPs
## 30                                                                                       Talk 2: Research Progress for Belowground Biomass & NPP
```


### Proposal workflow 

![showcase_proposal](./figure/static/showcase_proposal.png)

* caption: The paper proposal in its final approved state. The information on that page
           contains a title, a rational an envisaged date and journal. The calculated authors
           and email lists for communication as well as the attached datasets and sub
           projects involved (only partially shown). The proposal is published alredy see 
           (Lang et al. 2013).

If all data owners accepted the paper proposal `rbefdata` can be used to to
access the datasets. After setup we can start right away using data from the
proposal that we created. The proposal download function of `rbefdata` is used
for that. It draws all associated datasets of a proposal into the R environment
in one single step. It returns a list object that keeps a data frame per list
element containing a dataset of the proposal each (see blow).  The function
requires the ID of the proposal to work. The ID can be found in the URL of the
proposal (see box below).

```
# the proposal URL shows the id is 90 
http://befdataproduction.biow.uni-leipzig.de/paperproposals/90
```


```r
# proposal id is
datasets = bef.get.datasets_for_proposal(id = 90)
extract_second_dataset = datasets[[2]]
head(extract_first_dataset, 5)
```

```
## Error: object 'extract_first_dataset' not found
```


Each dataset in the `BEFdata` portal is associated with metadata the authors of
the dataset provide. We also provide access to the metadata from within
`rbefdata`. It can be accessed either directly via a metadata download command
that takes the ID of a dataset or extracted via the R internal `attributes()`
command. The extraction via attributes is possible as each dataset is attached
with its metadata when using one of the download commands of `rbefdata` (see
box below).


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


The dataset from the proposal contains three datasets, of which we do only use
the second and third. These two are written into two variables called
`Nretention` and `design` before deciding upon how to merge them. Inspecting
the headers of both dataset reveals each of them contains a column containing a
`plot_id` that seems suitable for merging. But we can also make use the
metadata for columns to check if this really is the case (see box below).


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


After merging the datasets the new synthesis dataset still contains many
columns not required for the analysis that can be dropped. To analyse the
dataset of system N retention we need information about the species diversity
in the plots and about which plot is placed in which block from the design
dataset. 'Species diversity' is used as a factor containing three levels (1,2,4
species mixtures). The response variables have been checked for normality with
`qqplot` and transformed (see box below).


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
## 2 - 1 == 0    1.053      0.293    3.59   0.0012 **
## 4 - 1 == 0    0.865      0.497    1.74   0.1841   
## 4 - 2 == 0   -0.188      0.479   -0.39   0.9163   
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
## 2 - 1 == 0   -0.294      0.127   -2.32     0.05 .
## 4 - 1 == 0   -0.499      0.215   -2.33     0.05 *
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


### Results of the showcase analysis

System 15N retention (overall plot recovery) was positively affected by species
richness at the level of P = 0.0576 (Chisq: 5.7; Fig. Xa). The analysis of the
different system compartments (leaves, fine roots and soil) revealed that fine
root recovery was lower than leaf recovery, and biomass recovery (leaves and
fine roots) was lower than soil recovery.  Whereas the relative leaf and root
recovery were significantly higher in species mixtures compared with
monoculture (Figs. Xb and Xc), the relative soil recovery was significantly
reduced (Fig. Xd).

Our results demonstrate that species richness of mixtures increases system N
retention in young subtropical tree plantations. Although relative soil
recovery was highest compared with relative leaf and root recovery, soil
recovery decreased with species richness (Fig. X). Thus, the observed positive
relationship between species richness and system N retention is caused by an
increase in relative N recovery of sapling biomass (fine roots and leaves) with
higher species numbers in mixtures. Our findings suggest positive species
diversity effects for an important ecosystem service, which is highly relevant
for afforestation programmes as currently applied in China on a large scale.
The positive relationship between species richness and system N retention
suggests that mixed plantings even at the sapling stage of a restricted species
pool may considerably increase N retention in subtropical forest systems even
after a few years. This in turn has the potential to significantly reduce N
losses and thus N accumulation in the leachate or groundwater (Lang et al.
2013).

![plot of chunk anne_final_plot](figure/anne_final_plot.png) 


* caption:  Nitrogen (N) retention affected by species richness. N retention summed as
            the recovery of soil, roots and leaves (a), relative leaf recovery (b), relative root
            recovery (c) and relative soil recovery (d). Significant differences as revealed by post
            hoc Tukey’s test (P < 0.05) are indicated by different letters.

Finally we need to decide on either to upload a full dataset which we could do
using the dataset upload function `bef.portal.upload.dataset()` or only to
upload the script and maybe a figure to highlight the road to the results from
the source datasets used. This can be done by attaching to the proposal with
`bef.portal.attach.to_proposal()`. For the example shown, it is the best way to
go with an attachment to the proposal as uploading the merged dataset would
only mean duplication of data in the database of the `BEFdata` platform.

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

* pros and cons of sending data to a local script or sending a script to a central database,
  - for researchers, it "feels" better, if the data are on the local machines
  - more freedom for researchers to use their tools of choice and to mix data with data from
    other sources
  - pros for sending a script to the data are efficiency, less network traffic
  - re-usability of scripts is easier, if they are sent to a central cluster, since everybody can
    do that.

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

There is a growing demand to effectively use and reuse available data which
puts much pressure on the development of software solutions that help
researchers not only to find but also to integrate heterogeneous small data
into a wider context (cite xxx). The software combination `rbefdata`/`BEFdata`
provides solutions to different parts of the data life cycle. On the `BEFdata`
side it covers data storage, metadata support and social components that foster
sharing data online in collaborations (cite Karin).  On `rbefdata` side the
combination offers easy access to data and metadata which helps to understand
and use data stored on a `BEFdata` platform.  Additionally it offers methods to
simply push back datasets and attachments like plots and scripts to the
`BEFdata` portal which is a stepping stone for reproducibility and data
provenance. 

The tag based exploration of datasets helps to find datasets relevant for a
certain analysis. The `tematres` vocabulary server integration further supports
this as it allows to retrieve term definitions as well as semantical relations
to broaden or narrow down search terms. This feature is part of the upcoming
integration of an ontology based on the vocabulary and knowledge of
Biodiversity Ecosystem Functioning Experiment

The `rbefdata` package makes the access to the data and metadata simple. The
availability available via the R statistics environment with allows for fast
analysis. The upload mechanisms of the package help to keep the Online platform
up to date and gives other researchers the possibility to reproduce the results
by downloading scripts attached to proposals. The uploaded script is not only a
stepping stone to reproducible research but also helps to track down data
provenance.

Especially domains with a high degree of interdisciplinary interactions and
heterogeneity in methods and data like ecology are facing problems in dealing
with some highly valuable concepts of data management like ontologies (e.g
                                                                       michener
                                                                       et al
                                                                       2012). 







We recently stared to develop an ontology using a `tematres` server containing
knowledge extracted from portals that deal with data management for ecological
research. The `tematres` server offers an API so all the contained terms can be
accessed by the upcoming version of `rbefdata`

The formalization developed will be based on the knowledge used in biodiversity
research. Thus we will here discuss the software combination `BEFdata` and
`rbefdata` in the light of the upcoming features and in general context state
of the art data management today. In one of the next versions to be rolled out
the `BEFdata` portal will get a semantical annotation feature.  This will give
administrators the ability to tag each column of datasets with a general term
that best describes the content. So the field will contain potential top terms
of the ontology. The tagging will be reflected in the API and can thus be
simply queried to use the information within the R package.  Using the
knowledge about the content of a column in the R package will enable us to do
support smart merges that work.

`tematres` ([homepage](http://www.vocabularyserver.com/))into `BEFdata` and the
`rbefdata` package so they play well together semantically.
    
While well described data can help a lot in understanding datasets and on
deciding upon the relevance and applicability in a certain analysis there is
still lots of manual intervention necessary after that to prepare the data for
analysis (cite Karin and me? or xxx). It may needs to be cleaned, imputed,
reshaped and merged which usually takes up to 70% of an analysis workflow,
before smart models can be applied to the data to find interesting patters
(cite the workflow paper of Karin and me). This preparatory steps not only are
time and labour intensive but also potentially error prone, especially as the
complexity of the analyses increases.

Those potentially can be used to improve or automate some of the most common
tasks in analyses starting from finding relevant data to cleaning and merging
as well as they can facilitate the exchange of data.  

Ontologies, as formal representations of knowledge, potentially offer a
sophisticated tool to deal with that step of data preparation (cite supporting
ecology as data intensive science). While they are already used in some
research domains like genetics (cite xxx, eg. http://www.geneontology.org/),
other domains face more problems using it (cite xxx, morpho team announced
semantic tagging but the plug-in did not appear anywhere). The application of
ontologies in ecology is discussed controversially (cite xxx) and it is argued
that they can be a huge benefit, but it is hard to set up a sophisticated
ontology covering all necessary terms and relation of a highly complex research
domains (cite xxx).




While data storage and description is almost the same for all kind of data the
effective interlinking of data via an ontology requires the development of a
common terminology all contributing scientist of a research domain accept and
not only use but help do develop and discuss it.  Thus collaborative ontology
engineering approaches like `ontoverse` (Zoulfa El Jerroudi et al. 2008) or
`tematres` are highly valuable as the not only help to set up ontologies but
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

