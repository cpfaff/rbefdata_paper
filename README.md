## rbefdata paper

* Tentative title:

`rbefdata` a package to access and process data stored on a BEFdata portal instance

* Journal:

???

### Read the paper

You can have a first glance on the contents in nice formatted markdown if you go
to the [markdown representation](paper/rbefdata.md) of the paper in this repository.

### Description

This paper deals with rbefdata and discusses the functionality on a real
scenario with already published data.

## Authors

* Karin Nadrowski
* Anne Lang
* Claas-Thido Pfaff

## Technique

### Github collaboration

For the collaboration on github please create your own author branch for writing.

```
git checkout -b author_yourname
```

Work on that branch only and once and a while merge it into the master branch. This works
as follows:

* Checkout the master

```
git checkout master
```

* Pull for changes in master online and merge them in

```
git pull --rebase
```

* Merge in recent changes from your author branch (can be conflicted)

```
git merge author_yourname
```

* Push the merged version online

```
git push
```

* Checkout your author branch and work on

```
git push
```

* Repeat the steps after another part is finished.


### R Markdown and Markdown

The whole paper is written in R markdown. Markdown which is a lightweight
markup language. For a description of commands that are available in Markdown
see [here](http://markdown.de/syntax/). The R Markdown markup makes it easier
to handle the inclusion of the R packages commands and output. You can use
[R-Studio](http://www.rstudio.com/) to edit the document as it offers methods
to compile the document from R Markdown to markdown and then to other document
formats (e.g html) with the Knitr package.

* Using [R Markdown](http://www.rstudio.com/ide/docs/authoring/using_markdown)
