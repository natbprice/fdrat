
<!-- README.md is generated from README.Rmd. Please edit that file -->

# fdrat - Faster drat

<!-- badges: start -->
<!-- badges: end -->

## Purpose of fdrat Fork

The drat package `insertPackage()` function has a slow write speed
because it is based on base `file.copy` which has a small write buffer.
This issue is worse on Windows than Linux because the `file.copy` buffer
in C is smaller (512 vs 8192), but still may not be much of an issue.
However, the performance penalty is significant for cloud-based file
shares because there is some non-negligible overhead for each write
operation and the small buffer causes excessive write operations. The
issue is exaggerated even more when the R packages are much larger than
typical CRAN package sizes.

A simple solution is to replace base `file.copy` with `fs::file_copy`.
Unfortunately, this proposed change was not accepted in the drat package
repo ([Issue \#127](https://github.com/eddelbuettel/drat/issues/127),
[Issue \#128](https://github.com/eddelbuettel/drat/issues/127)) so this
fork was created to address this issue.

## Benchmarks

Example of benchmarking transfer speeds to [SMB file shares in Azure
Files](https://docs.microsoft.com/en-us/azure/storage/files/files-smb-protocol?tabs=azure-portal)
using small 1MB file.

``` r
microbenchmark::microbenchmark(
  "fs::file_copy" = {
    fs::file_copy("1MB.bin", "//fdrat.file.core.windows.net/fdrat/1MB.bin", overwrite = TRUE)
  },
  "file.copy" = {
    file.copy("1MB.bin", "//fdrat.file.core.windows.net/fdrat/1MB.bin", overwrite = TRUE)
  },
  times = 10L,
  unit = "s",
  control = list(order = "block")
)
#> Unit: seconds
#>           expr        min        lq       mean     median        uq       max
#>  fs::file_copy  0.6132894  0.617477  0.6745066  0.6194089  0.620811  1.148491
#>      file.copy 14.6344611 14.704471 14.7420529 14.7320842 14.786816 14.877549
#>  neval
#>     10
#>     10
```

## drat

See <https://eddelbuettel.github.io/drat/> for detailed documentation.
