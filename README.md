
<!-- README.md is generated from README.Rmd. Please edit that file -->
salic <a href='https://www.southwickassociates.com'><img src='man/figures/logo.jpg' align="right" height="70" /></a>
====================================================================================================================

The salic package includes a set of functions prepared by Southwick Associates for summarizing agency data, particularly for use in AFWA's national/regional dashboard effort. It's intended to simplify/standardize this process by providing a set of easy-to-use functions.

Installation
------------

Ensure a verson of R (&gt;= 3.5.0) is installed: <https://www.r-project.org/>

``` r
# Install dependencies
install.packages(c("dplyr", "data.table"))

# Install salic from binary executables
install.packages("bla bla") # for Windows
install.packages("bla bla") # for Mac

# Alternatively, install salic from source
install.packages("devtools")
devtools::install_github("southwick-associates/salic")
```

Usage
-----

See [Introduction to salic](https://southwick-associates.github.io/salic/articles/salic.html) (`vignette("salic")` from the R console).

A template workflow for national/regional dashboards is available at <https://github.com/southwick-associates/dashboard-template>

### Example: fishing participants

Using `rank_sale()`, `make_history()`, `est_part()` from `?salic`.

``` r
library(dplyr)
library(salic)
data(cust, lic, sale)

history <- lic %>% 
    filter(type %in% c("fish", "combo")) %>% 
    inner_join(sale, by = "lic_id") %>% 
    rank_sale() %>% 
    make_history(2008:2018, carry_vars = "res") %>% 
    left_join(cust, by = "cust_id")
    
recode_agecat(history) %>%
    filter(!agecat %in% c("0-17", "65+")) %>%
    est_part()
#> # A tibble: 11 x 3
#>    tot    year participants
#>    <chr> <int>        <int>
#>  1 All    2008         5449
#>  2 All    2009         6352
#>  3 All    2010         6403
#>  4 All    2011         6297
#>  5 All    2012         6514
#>  6 All    2013         6348
#>  7 All    2014         6794
#>  8 All    2015         6718
#>  9 All    2016         6675
#> 10 All    2017         6645
#> 11 All    2018         6318
```
