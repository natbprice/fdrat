
<!-- README.md is generated from README.Rmd. Please edit that file -->

# fdrat - Faster drat

<!-- badges: start -->
<!-- badges: end -->

## Purpose of fdrat Fork

The `drat::insertPackage()` function has a slow write speed because it
is based on `base::file.copy` which has a small write buffer (512 on
Window, 8192 on Linux). The performance penalty is significant for
cloud-based file shares because the small buffer causes excessive write
operations and there is some non-negligible overhead for each operation.
The issue is exaggerated even more when the R packages are much larger
than typical CRAN package sizes.

A simple solution is to replace base `file.copy` with `fs::file_copy`.
Unfortunately, this proposed change was not accepted in the drat package
repo ([Issue \#127](https://github.com/eddelbuettel/drat/issues/127),
[Issue \#128](https://github.com/eddelbuettel/drat/issues/128)) so this
fork was created to address this issue.

## Benchmarks

-   `fdrat::insertPackage` is 20-30% faster when inserting a very large
    package (178 MB) in local repo

``` r
repo <- tempdir()
writeLines("<!doctype html><title>empty</title>", con = file.path(repo, "index.html"))
microbenchmark::microbenchmark(
  "fdrat::insertPackage" = {
    fdrat::insertPackage("h2o_3.34.0.3.zip", repo)
  },
  "drat::insertPackage" = {
    drat::insertPackage("h2o_3.34.0.3.zip", repo)
  },
  times = 10L,
  unit = "s",
  control = list(order = "block")
)
#> Unit: seconds
#>                  expr      min       lq     mean   median       uq      max
#>  fdrat::insertPackage 1.241044 1.244540 1.472655 1.461975 1.577839 1.993014
#>   drat::insertPackage 1.606491 1.639911 1.820988 1.757199 1.943500 2.195597
#>  neval
#>     10
#>     10
```

-   `fdrat::insertPackage` is much faster when inserting a large package
    (0.703 MB) in cloud-based repo ([SMB file shares in Azure
    Files](https://docs.microsoft.com/en-us/azure/storage/files/files-smb-protocol?tabs=azure-portal))

``` r
microbenchmark::microbenchmark(
  "fdrat::insertPackage" = {
    fdrat::insertPackage("tidyverse_1.3.1.tar.gz", "//fdrat.file.core.windows.net/fdrat/drat")
  },
  "drat::insertPackage" = {
    drat::insertPackage("tidyverse_1.3.1.tar.gz", "//fdrat.file.core.windows.net/fdrat/drat")
  },
  times = 10L,
  unit = "s",
  control = list(order = "block")
)
#> Unit: seconds
#>                  expr       min       lq      mean    median        uq
#>  fdrat::insertPackage  5.044299  5.09818  5.494505  5.428903  5.685363
#>   drat::insertPackage 15.113289 15.36189 15.627046 15.544733 15.766561
#>        max neval
#>   6.366673    10
#>  16.731505    10
```

-   `fdrat::insertPackage` allows inserting very large packages (178 MB)
    in cloud-based repo which would be prohibitively time consuming
    using drat ([SMB file shares in Azure
    Files](https://docs.microsoft.com/en-us/azure/storage/files/files-smb-protocol?tabs=azure-portal))

``` r
microbenchmark::microbenchmark(
  "fdrat::insertPackage" = {
    fdrat::insertPackage("h2o_3.34.0.3.zip", "//fdrat.file.core.windows.net/fdrat/drat")
  },
  times = 1L,
  unit = "s",
  control = list(order = "block")
)
#> Unit: seconds
#>                  expr      min       lq     mean   median       uq      max
#>  fdrat::insertPackage 108.5613 108.5613 108.5613 108.5613 108.5613 108.5613
#>  neval
#>      1
```

## drat

See <https://eddelbuettel.github.io/drat/> for detailed documentation.
