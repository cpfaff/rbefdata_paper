## rbefdata paper

* Tentative title:

`rbefdata` a package to access and process data stored on a BEFdata portal instance

* Journal:

???

### Read the paper

You can have a first glance on the contents in nice formatted markdown if you
go to the [markdown representation](paper/rbefdata.md) of the paper in this
repository.

### Edit the paper

To edit the paper please work in the .Rmd file in the paper folder as it is the
original file. Changes in this fle will be overwritten if i start a compilation
(knitr) run to the .md file and to the .html file. Here a link to the right
file:

[R markdown representation](paper/rbefdata.Rmd)


### Description

This paper deals with rbefdata and discusses the functionality on a real
scenario with already published data.

## Authors

* Karin Nadrowski
* Anne Lang
* Claas-Thido Pfaff
* xingxing man (sorry if this is not exactly right)

## Technique

### Github collaboration

For the collaboration on github please create your own author branch for writing.

```
git checkout -b author_yourname
```

Work on that branch only and once and a while merge it into the master branch.
This works as follows:

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


NOTE:

If you have conflicts on merging files with git you need to resolve them
manually. This is usually best done in a 3 way merge tool. Conflicts happen if
a part of document is modified in both the aim and the version you like to
merge in. You need to pick the changes you like to keep then manually.

### R Markdown and Markdown

The whole paper is written in R markdown. Markdown which is a lightweight
markup language. For a description of commands that are available in Markdown
see [here](http://markdown.de/syntax/). The R Markdown markup makes it easier
to handle the inclusion of the R packages commands and output. You can use
[R-Studio](http://www.rstudio.com/) to edit the document as it offers methods
to compile the document from R Markdown to markdown and then to other document
formats (e.g html) with the Knitr package.

* Using [R Markdown](http://www.rstudio.com/ide/docs/authoring/using_markdown)


### Work with rbefdata

As the rbefdata quires you to set your credentials to authenticate against the
BEFdata portal you need to set them somewhere. But as they are like passwords
you should not set it in the files that will be pushed to GitHub. For this I
created `.gitignore` file that makes the repository ignore a `secretes.R` file
in the `paper` folder. After download create it and add a line into it like
this but replace with your real credentials.

```
bef.options("user_credentials" = "s0l0p982340987uöaf")
```
