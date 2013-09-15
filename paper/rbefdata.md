## Introduction 

* We have lots of data available 
* Data is heterogeneous 
* Needs smart tools to find and merge (synthesis)

## Material and Methods 

### BEFdata portal

The BEFdata portal is a data management platform developed within the 
BEF-China project (FOR xxx) of the german science foundation. It offers 
tools for data harmonization...

### Data used

The data used for the presentation of this package stems from ...

### Rbefdata

The `rbefdata` package offers an option list that is used to determine 
the servers URLs the package contacts to to retrieve data, the download 
forlder name for attached freeformat content of a dataset and 

* load the package


```r
require(rbefdata)
```

```
## Loading required package: rbefdata
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
bef.options("user_credentials")
```

```
## [1] ""
```


* set options 


```r
bef.options(user_credentials = "aölkjspoiul12")
bef.options(url = "http://my.own.befdat.instance.com")
```


* get datasets 

In the very heart of the BEFdata portal there is a paper proposal process integrated. You shop together 
datasets and afterwards create a paper proposal based on the shopped dataset. In the proposal
you have to give information like a title for the proposal and a rationale describing how you 
intend to use the data and where and when to publish the results. If the proposal is handed in 
the authors will be informed that somebody likes to access their datasets and they can decide 
if they like to participate and how. After all authors have granted access on is good to go 
with the `rbefdata` package. One can draw all datasets associated to a proposal in one turn 
with the package.


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

The BEFdata portal offers metadat in Ecological Metadata Language format standard for download. 
This is used in the `rbefdata` package to associate a downloaded dataset with informations that
are required to understand a dataset. This information can be extracted from a dataset with 
the R command `attributes()`


```r
metadata = bef.portal.get.dataset_for_proposal(id = 1)
```

```
## Error: could not find function "bef.portal.get.dataset_for_proposal"
```


## Results 

## Discussion
