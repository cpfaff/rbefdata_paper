


## Abstract

Today we face a deluge of data scientists need to deal with in many different
disciplines. While there are already good solutions to some parts of the data
life cycle the applicability of the solutions to certain scientific domains
often varies. Especially research domains with a high degree of
interdisciplinary interactions and heterogeneity in methods and data like
ecology are facing problems in dealing with some valuable concepts like
ontologies that potentially can be used to improve or automate some of the most
common tasks in analyses like finding relevant data, cleaning and merging and a
exchange of datasets. We here introduce the `rbefata` package that connects to
the open source data management platform `BEFdata` that has been developed and
is used within the BEF-China experiment. We show the use of the package in
interaction with the data management platform by an example workflow that
integrates two datasets from the BEF-China experiment where the workflow is
representing an analysis that has been published already. Finally we discuss
this software combination in the context of current and future data management
requirements and the data life cycle. We also give an outlook on upcoming
features like a semantical assisted searches and merging of data to be
integrated with `rbefdata` and `BEFdata`.

## Introduction

With a growing awareness on the value of data, much effort has been put into
building data management platforms, to preserve all kind of environmental and
historic data, over the last years (e.g. diversity workbench, GBIF, `BEFdata`,
DataONE, LifeWatch). Many solutions for different scientific disciplines
appeared that provide data management plans for small scale projects or
collaborations as well as for large data producing long term or remote sensing
projects. An ongoing trend in that context is the development of integrative
databases or data portals. They serve as nodes that collect data from smaller
databases of a certain domain and they give researchers of that domain the
opportunity to access a wide range of relevant data all from one place. These
data management portals in fact offer a solution to to one of the most pressing
problems that we face with our valuable data today, their loss.

With a growing global data pool there is a also a growing demand to use and
reuse available data and to embed small heterogeneous data into a wider
context. A problem here is the legibility of datasets. Usually plain datasets
say nothing, to one who is not familiar with it and they are even hard to
decipher by the author himself after some time has passed. It is usually hard
to remember exactly what methods have been used to collect a certain columns
data or what the abbreviations or headers in the dataset mean. To solve this
problem metadata frameworks have been developed and published as standards so
nobody really needs to think about an own set of requirements to describe their
data. The Ecological Metadata Language
[EML](http://knb.ecoinformatics.org/software/eml/) is only one example for
that. While this theoretically solves the problem with not well described
datasets it is still hard to make researchers use it extensively as this
usually always means to learn new tools that help with the description process
(e.g morpho, data up).

We here introduce the R package `rbefdata` as part of the rOpenSci initiative
which aim is to give the R - Users all the flexibility of data access through
APIs. Our package connects the R statistics environment to the data management
platform `BEFdata`. It takes over the part of communicating with the data
platform in terms of up and download of datasets as well as it provides methods
to access the metadata provided by the dataset authors. Additionally it offers
methods that enable the exploration of datasets by keyword associations and the
download and upload of attachment files like R scripts or figures to datasets
in the portal.

We showcase the functionality of the package available with version `0.3.5`
creating a workflow that integrates two datasets. The use case is dealing with
data from a small scale experiment called pilot experiment in the BEF-China
experiment. It is a 15N tracer experiment which aims to disentangle the effect
of species mixtures on system N retention. The workflow depicts how to pull
data into the R environment, the inspection of datasets metadata and how to
upload data and attachments. It reconstructs a facet of an analysis that has
been published already (cite Anne Lang). The use case is dealing with data from
a small scale experiment called pilot experiment. It is a 15N tracer experiment
which aims to disentangle the effect of species mixtures on system N retention.


## Material and Methods

### BEF-China and the BEFdata portal

BEFdata, including the rbefdata package, has been developed within the
BEF-China experiment.  The BEF-China experiment is a Biodiversity Ecosystem
Functioning (BEF) experiment funded by the German science foundation (DFG, FOR
891). Experimental sites are located in the subtropics of China in the
provinces Jianxi and Zhejiang. The BEF-China research group (www.bef-china.de)
uses two main research platforms.  An experimental forest diversity gradient of
50~ha, and 27 observational plots of 30x30 m each located in the Gutianshan
Nature Reserve.  The observational plots were selected according to a crossed
sampling design along tree species richness and stand age. The data for the
workflow on carbon pools stems from 22 to 116 years consisting of 14 to 35
species (cite Bruelheide, 2010).

The [BEFdata](http://befdataproduction.biow.uni-leipzig.de/) portal is an open
source data management platform developed within the BEF-China project. It
adheres to standards like the Ecological Metadata Language (cite xxx) for
describing datasets with metadata and is specialized in harmonizing small
heterogeneous data that usually has to be dealt with in BEF. But its
specialization makes it also very valuable to use in any other scientific
domain that needs to deal with complex small and heterogeneous data.

The portal offers a social component where researchers can shop datasets and
write a paper proposals based on the datasets in their shopping cart. In the
process of creating a proposal some information like a title, a rationale, an
envisaged journal and date needs to be provided. Sending in a proposal a
researcher asks for access to the datasets and provides the data owners with
necessary information about the paper. The data owners then can decide if and
how they like to participate in the upcoming paper or if they only like to get
acknowledged for providing their data (cite Karin).

### The proposal

The portal facilitates research cooperation by the tool of paper proposals.
Sending in a proposal, a researcher asks for access to the datasets and
proposes his/her research idea to the dataowners and possible collaborators.
This more social component of the portal allows to include and acknowledge all
researchers involved in the data sampling process, promotes collaborations
between research units, avoids publication initiatives of the same research
ideas and adds to the transparency of data publication.  To create a paper
proposal the researcher can shop (select) datasets which are to be included in
the analyses.  Furthermore basic information of the proposed paper such as the
title, the rationale, the envisaged journal and date needs to be provided. The
data owners and proposed collaborators are informed and can decide if and how
they like to participate in the upcoming paper or if they only like to get
acknowledged for providing their data (cite Karin). Furthermore the datasets
assembled by the paper proposal can be readily imported in one step to the R
environment by rbefdata.


### rbefdata

The development of the `rbefdata` package started within the BEF-China project.
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

In this paper we use already published datasets (we should use more than one
dataset!, e.g. CSP for all, species reference, ...) as a use case to present
the functionalities and inter linkages between the BEF-China data portal and
`rbefdata`. Starting on with a paper proposal on following rationale.

!! Introduction !!

We created a paper proposal with the following rationale: 'Knowledge of
biodiversity effects on nutrient cycling patterns in subtropical forest
ecosystems is still very limited, particularly as regards macro nutrients such
as nitrogen and phosphorus. Experimental approaches using tree saplings may
promote an understanding of mechanisms that underlie nutrient acquisition and
cycling in early successional stages of secondary forests and forest
plantations.  Insights in the potential of nutrient retention of young tree
plantations are of particular interest in China, where large areas have been
reforested in order to counteract soil erosion and to increase the soils’ water
and nutrient retention capacity.  In this study we planted saplings of four
abundant early successional (evergreen and deciduous) tree species in
monocultures, two- and four-species combination to test the effect of species
richness on nitrogen acquisition and retention by using a 15N tracer
experiment.  A crucial question in BEF research is the appropriate time scale
of experiments which allows species richness effects to emerge. This question
gains importance when long-lived and slowly growing organisms such as trees are
considered. We wanted to analyse whether species richness effects occur during
the establishment phase of early successional tree species typical of
subtropical forests of China.  More precisely we wanted to test the following
hypotheses: (H1) Nitrogen acquisition and retention increases with species
richness due complementary effects in species mixtures.  (H2) Species richness
effects strengthen over time.' The respective proposal can be assessed under
(url) For a detailed description of the experimental design we refer to Lang et
al. 2013 (DOI)

!! use more than one datafile!.

In this case, there should be a separate file for plot attributes, soil
attributes, plot diversity, etc. , another one for species names!!

![showcase_proposal](./figure/static/showcase_proposal.png)

* caption: The paper proposal in its final approved state. The information on that page
           contains a title rational envisaged date and journal. The calculated authors
           and email lists for communication as well as the attached datasets and sub
           projects involved (only partially shown).


?? Is this based on a published paper? Then we should cite that paper!??

When all data owners accepted the paper proposal `rbefdata` can be used to
directly access the datasets from the data platform and transfer them to the R
environment. To do so the `rbefdata` package needs to be setup. This requires
installing, loading the package and setting the required package options.
Having a look into the options list reveals several fields that can be filled
in, like the URL to the `BEFdata` server, user credentials and a download
folder name that is used to store free format files attached to datasets. The
`tematres` server related URLs in the options are part of upcoming features
that are non fully functional on the time of writing and thus can be ignored by
now.

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
box below).

```
# the proposal URL shows the id is 90
http://befdataproduction.biow.uni-leipzig.de/paperproposals/90
```


```r
# proposal id is
datasets = bef.get.datasets_for_proposal(id = 90)
```

```
## Error: Couldn't resolve host 'china.befdata.biow.uni-leipzig.de'
```

```r
extract_second_dataset = datasets[[2]]
```

```
## Error: object 'datasets' not found
```

```r
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
## No such file or directoryfailed to load external entity "http://china.befdata.biow.uni-leipzig.de/datasets/335.eml?separate_category_columns=TRUE"
```

```
## Error: 1: No such file or directory2: failed to load external entity
## "http://china.befdata.biow.uni-leipzig.de/datasets/335.eml?separate_category_columns=TRUE"
```

```r

# extract title of first dataset in proposal
attributes(datasets[[1]])$title
```

```
## Error: object 'datasets' not found
```

```r

# extract all dataset titles in the proposal
titles = sapply(datasets, function(x) attributes(x)$title)
```

```
## Error: object 'datasets' not found
```

```r
titles
```

```
## Error: object 'titles' not found
```

```r

# other metadata available
names(attributes(datasets[[1]]))
```

```
## Error: object 'datasets' not found
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
```

```
## Error: object 'datasets' not found
```

```r
design = datasets[[3]]
```

```
## Error: object 'datasets' not found
```

```r

# overview about the contents of the datasets

# names in dataset Nretention
names(Nretention)
```

```
## Error: object 'Nretention' not found
```

```r

# description of column plot_id
Nretention_column_plot_id_description = attributes(Nretention)$columns[1, ]$description
```

```
## Error: object 'Nretention' not found
```

```r
Nretention_column_plot_id_description
```

```
## Error: object 'Nretention_column_plot_id_description' not found
```

```r

# names in dataset Nretention
names(design)
```

```
## Error: object 'design' not found
```

```r

design_column_plot_id_description = attributes(design)$columns[4, ]$description
```

```
## Error: object 'design' not found
```

```r
design_column_plot_id_description
```

```
## Error: object 'design_column_plot_id_description' not found
```


After merging the datasets the new synthesis dataset still contains many
columns not required for the analysis that can be dropped. To analyse the
dataset of system N retention we need information about the species diversity
in the plots and about which plot is placed in which block from the design
dataset. 'Species diversity' is used as a factor containing three levels (1,2,4
species mixtures). The response variables have been checked for normality with
`qqplot` and transformed (box below).

!! Very cool!!!



```r
# the synthesis dataset
syndata = merge(Nretention, design)
```

```
## Error: object 'Nretention' not found
```

```r

# overview about the content of the synthesis dataset
names(syndata)
```

```
## Error: object 'syndata' not found
```

```r

# remove unwanted variables from synthesis datset
syndata = syndata[-c(9:14, 16:41)]
```

```
## Error: object 'syndata' not found
```

```r
names(syndata)
```

```
## Error: object 'syndata' not found
```

```r

# > we want to use 'species_diversity' as a factor
syndata$species_diversity = as.factor(syndata$species_diversity)
```

```
## Error: object 'syndata' not found
```

```r

# square root transforme response variables
syndata$recov_plot_t = syndata$recov_plot^0.5
```

```
## Error: object 'syndata' not found
```

```r
syndata$perleaf_plot_t = syndata$perleaf_plot^0.5
```

```
## Error: object 'syndata' not found
```

```r
syndata$perroot_plot_t = syndata$perroot_plot^0.5
```

```
## Error: object 'syndata' not found
```

```r
syndata$persoil_plot_t = syndata$persoil_plot^0.5
```

```
## Error: object 'syndata' not found
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
```

```
## Error: object 'syndata' not found
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
## Error: no 'model.matrix' method for 'model' found!
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
## Error: object 'syndata' not found
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
## Error: no 'model.matrix' method for 'model' found!
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
## Error: object 'syndata' not found
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
## Error: no 'model.matrix' method for 'model' found!
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
## Error: object 'syndata' not found
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
## Error: no 'model.matrix' method for 'model' found!
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


### Results of the showcase analysis

System 15N retention (overall plot recovery) was positively affected by species
richness at the level of P = 0.l0576 (Chisq: 5.7; Fig. Xa). The analysis of the
different system compartments (leaves, fine roots and soil) revealed that fine
root recovery was lower than leaf recovery, and biomass recovery (leaves and
fine roots) was lower than soil recovery.  Whereas the relative leaf and root
recovery were significantly higher in species mixtures compared with
monocultures (Figs. Xb and Xc), the relative soil recovery was significantly
reduced (Fig. Xd).


?? This should have been reported elsewhere! This paper should be cited here!!


?? was the general aim of the analysis part of the introduction? It should be!!

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

!! This is really well done!!



```
## Error: object 'syndata' not found
```

```
## Error: object 'recov_plot' not found
```

```
## Error: plot.new has not been called yet
```

```
## Error: object 'perleaf_plot' not found
```

```
## Error: plot.new has not been called yet
```

```
## Error: object 'perroot_plot' not found
```

```
## Error: plot.new has not been called yet
```

```
## Error: object 'persoil_plot' not found
```

```
## Error: plot.new has not been called yet
```


* caption:  Nitrogen (N) retention affected by species richness. N retention summed as
            the recovery of soil, roots and leaves (a), relative leaf recovery (b), relative root
            recovery (c) and relative soil recovery (d). Significant differences as revealed by post
            hoc Tukey’s test (P < 0.05) are indicated by different letters.

Finally we need to decide on either to upload a full dataset which we could do
using the dataset upload function `bef.portal.upload.dataset()` or only to
upload the script and maybe a figure to highlight the road to the results
starting from the source datasets used. This can be done by attaching to the
proposal with `bef.portal.attach.to_proposal()`.

For the shown example it is the best way to go with an attachment to the
proposal as uploading the merged dataset would only mean duplication of data in
the database of the data management platform.

!! no! Upload!. There should be some new data, maybe on plot level, maybe on species level.
Maybe something such as general N uptake at median species diversity for the species in
question, that can then be used by other projects as functional traits. Upload data!

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
# caption for the figure
caption = "Nitrogen (N) retention affected by species richness. N retention summed as\n           the recovery of soil, roots and leaves (a), relative leaf recovery (b), relative root\n           recovery (c) and relative soil recovery (d). Significant differences as revealed by post\n           hoc Tukey’s test (P < 0.05) are indicated by different letters."

# upload the figure
bef.portal.attach.to_proposal(id = 90, attachment = file.path(tempdir(), "results_plot_proposal_90.png"),
    description = caption)
```

```
## Error: specified file does not exist: /tmp/RtmpwjKr5z/results_plot_proposal_90.png.  You must
## specify a valid file name or provide the contents to send.
```


![showcase_proposal_attachment](./figure/static/showcase_proposal_attachments.png)

* caption: The paper proposal in its final approved state with attachments. The
           attachments are the final plot and the R script that has been used to derive
           the resutls in the published paper.

## Discussion

* up to now no use of the thesaurus! If this stays as such, all the passages on ontologies have
  to be removed! So try to integrate the use of thesauri! Then ontologies can be discussed. But
  ontologies should not have such a high prominence in the introduction.

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

As there is a growing demand to effectively reuse available data this puts much
pressure on the development of solutions that help researchers not only to find
but also to integrate heterogeneous small data into a wider context. Highly
interdisciplinary research domains like ecology are challenging in terms of
data reuse and exchange. While data storage and description is almost the same
for all kind of data the effective interlinking of data via an ontology
requires the development of a common terminology all contributing scientist of
a research domain accept and not only use but help do develop and discuss it.
Thus collaborative ontology engineering approaches like `ontoverse`
(Zoulfa El Jerroudi et al. 2008) or `tematres` are highly valuable as the not
only help to set up ontologies but also to develop and maintain them over time
even if the researchers change that contribute to it.

The software combination of `rbefdata` and `BEFdata` offers a solutions to data
storage for different sizes of projects, it helps in describing data with
metadata and to provide a public with the information via the EMl metadata
standard, it fosters the collaboration and the trust in sharing data online by
paper proposals and the helps in analysing by offering simple tools to pull
data right direct from the portal into the R statistics environment. The upload
functionality provided by `rbefdata`

(metadata)
    + collaboration (data sharing)
    + simply pull data into analysis software and push data back
    + data provenance by attaching R scripts to uploads


(data intensive science, long tail). The
combination of `BEFdata` and the `rbefdata` package provides solutions to parts
of the data lifecycle as it deals with finding and describing data as well as
the as it promotes the understanding and reuse of data, as it is adhering
metadata standards.

a one part of the data life cycle and especially introduces a solution to deal
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



