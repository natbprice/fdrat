## fdrat: Fast Drat R Archive Template

*Purpose of fdrat Fork:*

The R base `file.copy` function is very slow with (Windows?) network drives so I 
replaced it with `fs::file_copy`. In my testing, transfer speeds were about 50X faster
on a 200 MB file.

This package will become obsolete if the performance
of `file.copy` is improved in future R versions or a workaround is added in
[drat](https://github.com/eddelbuettel/drat) ([Issue #127](https://github.com/eddelbuettel/drat/issues/127)).

> **drat**
>
> What cute people say when they are pissed off
>
> _"Oh Drat, i lost my wallet"_
>
> [Urban Dictionary](https://www.urbandictionary.com/define.php?term=drat)

### Nota Bene

Do **not** fork _this_ repo as a quick start towards creating your `drat`, fork [this
repo](https://github.com/drat-base/drat) instead. See below for more.

### Background

The R package ecosystem is one of the cornerstones of the success seen by R.
As of July 2020, over 16000 packages are on [CRAN](https://cran.r-project.org),
with about one thousand more at [BioConductor](https://www.bioconductor.org).

Support for multiple repositories is built deeply into R; mostly via the
(default) package `utils`. The
[`update.packages`](https://www.rdocumentation.org/packages/utils/functions/update.packages)
function (along with several others from the `utils` package) can be used with
ease for these three default repositories as well as many others. But it
seemed that support for _simple creation and use_ of local repositories was
missing.

[Drat](https://dirk.eddelbuettel.com/code/drat.html) tries to help here and supports two principal modes:

- *GitHub* by leveraging `gh-pages`
- *Other repos* by using other storage where you can write and provide html access

Please see the next section about how to get started, the package documentation, the
[drat package page](https://dirk.eddelbuettel.com/code/drat.html) or the
[blog section on drat](http://dirk.eddelbuettel.com/blog/code/drat/) for more.

### Getting Started

Do **not** fork _this_ repo as a quick start towards creating your `drat`, fork [this
repo](https://github.com/drat-base/drat) instead. See below for more.

See the vignettes

- [Drat FAQ](https://eddelbuettel.github.io/drat/vignettes/dratfaq/),
- [Drat for Package Authors](https://eddelbuettel.github.io/drat/vignettes/dratforauthors/),
- [Drat for Package Users](https://eddelbuettel.github.io/drat/vignettes/dratforusers/)
- [Drat Step by Step](https://eddelbuettel.github.io/drat/vignettes/dratstepbystep/)
- [Why Drat?](https://eddelbuettel.github.io/drat/vignettes/whydrat/)
- [Combining Drat and Travis](https://eddelbuettel.github.io/drat/vignettes/combiningdratandtravis/)
- [Drat Lightning Talk at useR!2015](https://dirk.eddelbuettel.com/papers/useR2015_drat.pdf)

for the FAQ, two principal uses cases, basic motivation and an overview / introduction.
The package documentation provides more details.  The
[drat package page](https://dirk.eddelbuettel.com/code/drat.html) has a longer
tutorial, and the
[blog section on drat](http://dirk.eddelbuettel.com/blog/code/drat/) has even
more.

Package documentation, help pages, vignettes, and more is also available
[here](https://eddelbuettel.github.io/drat/).



### Installation

The preferred approach is to install the released package from [CRAN](https://cran.r-project.org) via the standard

```{.r}
install.packages("drat")
```

command.


### Quick Start Towards Your Own Drat

`drat` comes with its own repo creation helper function
[`initRepo`](https://eddelbuettel.github.io/drat/man/initRepo/), but an even shorter path may be to
fork an existing repo.  This has been done numerous times with this original repo. However, over
time this repo accumulated code refinements along with more documentation making it a little
unwieldy. So we set up [dedicated repo](https://github.com/drat-base/drat) just to facilitate `drat`
forking.  Clone it, and you will have a ready-to-use `drat` repository.

### Status

The package has been available from [CRAN](https://cran.r-project.org) since
the Spring of 2015 and starting to get some use. Possible improvements,
additions and next steps are listed in the
[TODO.md](https://github.com/eddelbuettel/drat/blob/master/inst/TODO.md)
file.

A few drat repositories are starting to appear (besides this one). An incomplete list (looking at the direct forks as well as GitHub search):

 - [yutannihilation](https://github.com/yutannihilation/drat)
 - [gschofl](https://github.com/gschofl/drat/)
 - [csgillespie](https://github.com/csgillespie/drat)
 - [shabbychef](https://github.com/shabbychef/drat)
 - [RcppCore](https://github.com/RcppCore/drat)
 - [arilamstein](https://github.com/arilamstein/drat)
 - [piccolbo](https://github.com/piccolbo/drat)
 - [ghrr](https://github.com/ghrr/drat)
 - [cloudyr](https://cloudyr.github.io/drat/)
 - [dmlc](https://github.com/dmlc/drat)
 - [thospfuller](https://github.com/thospfuller/drat)

The [rOpenSci](https://ropensci.org) project uses
[drat](https://dirk.eddelbuettel.com/code/drat.html) to distribute their code
and has written a
[nice blog post](https://ropensci.org/blog/2015/08/04/a-drat-repository-for-ropensci/)
about it.

### Travis Integration

Colin Gillespie has started to integrate [Travis CI](https://www.travis-ci.org) with drat, see his
[dratTravis](https://github.com/csgillespie/dratTravis) repository for more details, and the
contributed vignette [Combining Drat and Travis](https://eddelbuettel.github.io/drat/vignettes/combiningdratandtravis/)

### Author

Dirk Eddelbuettel, with contributions by Carl Boettiger, Sebastian Gibb, Colin Gillespie, Matt
Jones, Thomas Leeper, Steven Pav, Jan Schulz, Christoph Stepper, Felix G.M. Ernst, and Patrick
Schratz.

### License

GPL (>= 2)
