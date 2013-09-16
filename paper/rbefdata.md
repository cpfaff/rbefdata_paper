


## Abstract 

The story board:

* Huge amount of data available (deluge of data)
* More and more gets accessible (with some hindrances) 
    - metadata missing (renders data useless) 
    - lack of reward for data providers (people keep their data secret)
    - so lots of data gets still lost (needs help e.g rebind)
* Data often hard to find/reuse 
    - if not well described 
* But there is a growing need to reuse data 
    - so we need tools supporting researchers in doing so (reuse available)
* The BEFdata portal provides a good base for heterogeneous data in ecology  
    - we dock onto that with rbefdata to pull data into data statistics  
    - Data life cycle (we cover it partially focused and doing this well) 
        + BEFdata (Store data, Describe it with metadat, Collaborate and Share it)
        + rbefdata (Find and understand and analyse data as well as reuse of data). 
          
* Maybe also shorlty introduce the data lifecycle and use it to show to which 
  parts of that cycle we offer soutions.

## Introduction 

* data is valuable 
    - also in the long run  
    - there are solutions for data storage
    - and also nodes that collect the data 

With a growing awareness on the long term value of data, much effort has been
put into building data management platforms, to preserve all kind of
environmental and historic data, over the last years (e.g. diversity workbench,
BEFdata). Many specialized solutions for different scientific disciplines
appeared that provide data management plans for small scale projects or
collaborations as well as for large data producing long term or remote sensing
projects. An ongoing trend in that context is the development of integrative
databases or data portals. They serve as nodes that collect data from smaller
databases of a certain domain and they give researchers of that domain the
opportunity to access a wide range of relevant data from one place.  This
portals in fact offer a solution to to one of the most pressing problems that
we face with our valuable data today, their lost. 

* data reuse 
    - data needs to be reusable 
    - otherwise it is almost worthless
    - this needs metadata so others can understand what we have done

Another big problem with data, especially in terms of reuse of available data,
is the general understanding of datasets. Usually plain datasets say nothing,
to one who is not familiar with it and they are even hard to decipher by the
author itself after some time has passed. It is usually hard to remember
exactly what methods have been used to collect a certain columns data or what
the abbreviations or headers in the dataset mean. To solve this this problem
metadata frameworks have been developed and published as standards so nobody
really needs to think about an own set of requirements to describe its data.
The Ecological Metadata Language is only one example for that. While this
theoretically solves the problem with not well described datasets it is still
hard to make people use it extensively as this usually always means to learn
new tools that help with the description process.

* find/merge and prepare data takes time   
    - ontologies are discussed controversially in ecology 
    - on one hand they offer a solid backbone to develop smart software
    - on the other hand they are they are hard to create especially 
      for a high heterogeneous reaearch domain like ecology.

While well described data helps a lot in understanding datasets and on deciding
upon the relevance and applicability in a certain meta analysis there is still
lots of manual intervention necessary after that to prepare the data for
analysis. It may needs to be cleaned, imputed, reshaped and merged which
usually takes up to 70% of the analysis workflow, before the smart models can
be applied to the data to find interring patters (cite the workflow paper of
Karin and me). This preparation steps are not only time and labour intensive
but also potentially error prone, especially as the complexity of analyses
grows. 

* Ontologies are either already used or discussed controversially 
  - ontologies are used to capture knowledge as formal representations of domain knowledge
  - they can be used to develop smart software 
  - smart software can help 
    + in finding relevant data 
    + merge and prepare heterogeneous data for analysis

Ontologies, formal representations of knowledge potentially offer a
sophisticated tool to deal with that step of data preparation. While they are
already used in some research domains like genetics, other domains face more
problems using it. For example, ecology has grown into a more collaborative,
interdisciplinary and data intensive science over the last decade, to address
questions on a greater temporal and spatial scale (e.g michener et al 2012).
The data here is mainly provided by small scale studies spread all over the
world (e.g heidorn2009 shedding light on the dark) but also through bigger long
term projects like LTER (cite xxx), BEF-China (cite xxx), governmental projects
and local initiatives (cite xxx). This in fact results in a wild growing,
complex and heterogeneous data landscape in that we need to deal with. The
application of ontologies in ecology is discussed controversially (cite xxx)
which is mainly related to the heterogeneity of the research domain and it is
argued that they can be a benefit but it is hard to set up a versatile ontology
covering all necessary terms of a complex research domain like ecology.

* rbefdata in combination with BEFdata provide solutions to a parts of the data
  life cycle in ecology:
    - store data 
    - describe the data (metadata) 
    - share data and 
    - find relevant data 
    - get the data into Statistics software 

There is a growing demand to use data already available and here we present you
one software solution that deals with it. We introduce the rbefdata package as
companion package to the data management platform BEFdata of the BEF-China
project (cite Karin). We demonstrate a workflow that shows the integration of
xxx datasets from the BEF-China project and. For that we use data that already
has been published and is open access so everybody will be able to reproduce
the workflow presented here. 

The combination of both tools offers solutions to the data life cycle
in terms of storing, describing and sharing data.  The rbefdata package makes
the data available 



think of ways on how to make the most out of the data we already have before we
start to collect more data in general or even worse repeat to pick up data that
already has been collected by someone else.

Another problem with data is putting data into a public accessible database is
a good step for long term preservation this is only the first step. 

While some research disciples do very well with the solutions available (e.g
Genetics), others facing more problems. 

The integration of dataset into meta analyses is still a very time and labour
intensive process. 

which is
error prone especially with a growing heterogeneity of the underlying data.

Ontology needs also be discussed here a bit more intensive... 

Ontologies can play an important role as they potentially offer a backbones for
the development of smart tools helping researchers to find and merge data (cite
XXX). But their application in ecology is discussed controversially as
capturing the knowledge of ecology in a formal representation can be highly
complex for a interdisciplinary research domains. 


## Material and Methods 

### BEFdata portal

The BEFdata portal (cite Kain,
[url](http://befdataproduction.biow.uni-leipzig.de/)) is a data management
platform developed within the BEF-China project (FOR 891) which is funded by
the German science foundation. The BEF China experiment is a ... (should I go
into details here?)

The BEFdata platform is specialized in harmonizing small heterogeneous data
that usually has to be dealt with in biodiversity ecosystem functioning but
also in other parts of ecological research. The portal offers a social
component that lowers the hurdles on sharing data online and tools that help
researchers to describe their data with metadata.

### Data used

The data used for the presentation of this package stems from (A. Lang. ...)
from the BEFdata portal. The data is free as it already was published.

### Rbefdata

The `rbefdata` package offers an option list that is used to determine the
servers URLs the package contacts to to retrieve data, the download folder name
for attached free format content of a dataset and 

* load the package


```r
require(rbefdata)
```


* list options


```r
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


* query options


```r
bef.options("url")
```

```
## [1] "http://china.befdata.biow.uni-leipzig.de"
```


* set options 


```r
bef.options(user_credentials = "aölkjspoiul12")
bef.options(url = "http://my.own.befdat.instance.com")
```





Introduction to the rbefdata R package

* get datasets 

In the very heart of the BEFdata portal there is a paper proposal process
integrated. You shop together datasets and afterwards create a paper proposal
based on the shopped dataset. In the proposal you have to give information like
a title for the proposal and a rationale describing how you intend to use the
data and where and when to publish the results. If the proposal is handed in
the authors will be informed that somebody likes to access their datasets and
they can decide if they like to participate and how. After all authors have
granted access on is good to go with the `rbefdata` package. One can draw all
datasets associated to a proposal in one turn with the package.


```r
dataset_list = bef.portal.get.datasets_for_proposal(id = 1)
```

```
## Error: Not Found
```

```r
extract_one_dataset = dataset_list[[1]]
```

```
## Error: object 'dataset_list' not found
```


* Inspect datasets

The BEFdata portal offers metadat in Ecological Metadata Language format
standard for download (cite EML). We make use of that metadata in the`rbefdata`
package as well and each dataset is associated with its metadata on download.
So you always have acces to the information that is required to understand a
dataset. This information can be extracted from a dataset with the R command
`attributes()`


```r
dataset_list = bef.portal.get.dataset_for_proposal(id = 1)
```

```
## Error: could not find function "bef.portal.get.dataset_for_proposal"
```

```r
attributes(dataset_list[[1]])$title
```

```
## Error: object 'dataset_list' not found
```

* write your scripts 


* vizualize the portal (keywords) 

see figure ... in appendix

## Results

The results presents a usecase maybe we just rename results to usecase and
introduce the data used in the material and methods section. 

## Discussion

Discussion will be in the light of future features like the upcomming
integration of tematres into BEFdata and the rbefdata package so they play well
together semantically.

## Appendix

### Figures 


```r

bef.portal.vizualize.keywords()
```

```
## Warning: shannon diversity could not be fit on page. It will not be
## plotted. Warning: wood perforation plates could not be fit on page. It
## will not be plotted. Warning: BEF China PIs could not be fit on page. It
## will not be plotted. Warning: biomass allocation could not be fit on page.
## It will not be plotted. Warning: cadmium at wavelength 214nm could not be
## fit on page. It will not be plotted. Warning: cadmium at wavelength 228nm
## could not be fit on page. It will not be plotted. Warning: experimental
## design could not be fit on page. It will not be plotted. Warning:
## geomorphology could not be fit on page. It will not be plotted. Warning:
## intraspecific diversity could not be fit on page. It will not be plotted.
## Warning: leaf physical resistance could not be fit on page. It will not be
## plotted. Warning: phylogenetic diversity could not be fit on page. It will
## not be plotted. Warning: response variable could not be fit on page. It
## will not be plotted. Warning: secondary compounds could not be fit on
## page. It will not be plotted. Warning: spatial genetic structure could not
## be fit on page. It will not be plotted. Warning: species trait could not
## be fit on page. It will not be plotted. Warning: trait dissimilarity could
## not be fit on page. It will not be plotted. Warning: wood compression
## could not be fit on page. It will not be plotted. Warning: wood shrinkage
## could not be fit on page. It will not be plotted. Warning: wood stretching
## could not be fit on page. It will not be plotted. Warning: aboveground
## biomass could not be fit on page. It will not be plotted. Warning:
## aeromorphic organic layer could not be fit on page. It will not be
## plotted. Warning: BEF China projects could not be fit on page. It will not
## be plotted. Warning: below ground could not be fit on page. It will not be
## plotted. Warning: cavity nesting hymenoptera could not be fit on page. It
## will not be plotted. Warning: coarse root density could not be fit on
## page. It will not be plotted. Warning: community similarity could not be
## fit on page. It will not be plotted. Warning: crown projection area could
## not be fit on page. It will not be plotted. Warning: eco-physiologic
## traits could not be fit on page. It will not be plotted. Warning:
## ecosystem functioning could not be fit on page. It will not be plotted.
## Warning: experimental treatment could not be fit on page. It will not be
## plotted. Warning: growth rings could not be fit on page. It will not be
## plotted. Warning: hunting type could not be fit on page. It will not be
## plotted. Warning: laboratories could not be fit on page. It will not be
## plotted. Warning: land use history could not be fit on page. It will not
## be plotted. Warning: mixed models could not be fit on page. It will not be
## plotted. Warning: multi-trophic interactions could not be fit on page. It
## will not be plotted. Warning: nitrogen cycling could not be fit on page.
## It will not be plotted. Warning: non-random extinction could not be fit on
## page. It will not be plotted. Warning: parasitoids could not be fit on
## page. It will not be plotted. Warning: phylogenetic distinctness could not
## be fit on page. It will not be plotted. Warning: phytophagous insects
## could not be fit on page. It will not be plotted. Warning: PI meeting
## could not be fit on page. It will not be plotted. Warning: predators could
## not be fit on page. It will not be plotted. Warning: rainfall simulator
## could not be fit on page. It will not be plotted. Warning: research
## proposals could not be fit on page. It will not be plotted. Warning:
## respiration could not be fit on page. It will not be plotted. Warning:
## rooting depth could not be fit on page. It will not be plotted. Warning:
## runoff plots could not be fit on page. It will not be plotted. Warning:
## simpson diversity could not be fit on page. It will not be plotted.
## Warning: snag height could not be fit on page. It will not be plotted.
## Warning: social status could not be fit on page. It will not be plotted.
## Warning: specialization could not be fit on page. It will not be plotted.
## Warning: species identity variable could not be fit on page. It will not
## be plotted. Warning: temperature could not be fit on page. It will not be
## plotted. Warning: topography could not be fit on page. It will not be
## plotted. Warning: tree crown could not be fit on page. It will not be
## plotted. Warning: vegetation stratum could not be fit on page. It will not
## be plotted. Warning: Weibull distribution could not be fit on page. It
## will not be plotted. Warning: wood ground tissue could not be fit on page.
## It will not be plotted. Warning: wood mechanics could not be fit on page.
## It will not be plotted. Warning: wood porosity could not be fit on page.
## It will not be plotted.
```

![plot of chunk vizalize_keywords](figure/vizalize_keywords.png) 

### Tables
