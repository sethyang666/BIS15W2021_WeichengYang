---
title: "Dummy Push"
author: "Seth Yang"
date: "2021-01-07"
output: 
  html_document: 
    keep_md: yes
---






## Install Packages

```r
options(repos = c(CRAN = "http://cran.rstudio.com"))
install.packages("tidyverse")
```

```
## package 'tidyverse' successfully unpacked and MD5 sums checked
## 
## The downloaded binary packages are in
## 	C:\Users\weich\AppData\Local\Temp\RtmpM76Yd9\downloaded_packages
```

```r
install.packages("nycflights13")
```

```
## package 'nycflights13' successfully unpacked and MD5 sums checked
## 
## The downloaded binary packages are in
## 	C:\Users\weich\AppData\Local\Temp\RtmpM76Yd9\downloaded_packages
```

```r
library(tidyverse)
```

```
## Warning: package 'tidyverse' was built under R version 4.0.3
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.3     v purrr   0.3.4
## v tibble  3.0.4     v dplyr   1.0.2
## v tidyr   1.1.2     v stringr 1.4.0
## v readr   1.4.0     v forcats 0.5.0
```

```
## Warning: package 'ggplot2' was built under R version 4.0.3
```

```
## Warning: package 'tibble' was built under R version 4.0.3
```

```
## Warning: package 'tidyr' was built under R version 4.0.3
```

```
## Warning: package 'readr' was built under R version 4.0.3
```

```
## Warning: package 'purrr' was built under R version 4.0.3
```

```
## Warning: package 'dplyr' was built under R version 4.0.3
```

```
## Warning: package 'forcats' was built under R version 4.0.3
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```


```r
install.packages("tidyverse")
```

```
## Warning: package 'tidyverse' is in use and will not be installed
```

## Working directory

```r
getwd()
```

```
## [1] "C:/Users/weich/OneDrive/Desktop/BIS15W2021_Seth/lab1"
```

## Session Info

```r
sessionInfo()
```

```
## R version 4.0.2 (2020-06-22)
## Platform: x86_64-w64-mingw32/x64 (64-bit)
## Running under: Windows 10 x64 (build 19041)
## 
## Matrix products: default
## 
## locale:
## [1] LC_COLLATE=English_United States.1252 
## [2] LC_CTYPE=English_United States.1252   
## [3] LC_MONETARY=English_United States.1252
## [4] LC_NUMERIC=C                          
## [5] LC_TIME=English_United States.1252    
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## other attached packages:
## [1] forcats_0.5.0   stringr_1.4.0   dplyr_1.0.2     purrr_0.3.4    
## [5] readr_1.4.0     tidyr_1.1.2     tibble_3.0.4    ggplot2_3.3.3  
## [9] tidyverse_1.3.0
## 
## loaded via a namespace (and not attached):
##  [1] Rcpp_1.0.5        cellranger_1.1.0  pillar_1.4.7      compiler_4.0.2   
##  [5] dbplyr_2.0.0      tools_4.0.2       digest_0.6.25     lubridate_1.7.9.2
##  [9] jsonlite_1.7.1    evaluate_0.14     lifecycle_0.2.0   gtable_0.3.0     
## [13] pkgconfig_2.0.3   rlang_0.4.7       reprex_0.3.0      cli_2.2.0        
## [17] rstudioapi_0.13   DBI_1.1.0         yaml_2.2.1        haven_2.3.1      
## [21] xfun_0.18         withr_2.3.0       xml2_1.3.2        httr_1.4.2       
## [25] knitr_1.30        fs_1.5.0          generics_0.1.0    vctrs_0.3.6      
## [29] hms_0.5.3         grid_4.0.2        tidyselect_1.1.0  glue_1.4.2       
## [33] R6_2.5.0          fansi_0.4.1       readxl_1.3.1      rmarkdown_2.4    
## [37] modelr_0.1.8      magrittr_1.5      backports_1.1.10  scales_1.1.1     
## [41] ellipsis_0.3.1    htmltools_0.5.0   rvest_0.3.6       assertthat_0.2.1 
## [45] colorspace_2.0-0  stringi_1.5.3     munsell_0.5.0     broom_0.7.3      
## [49] crayon_1.3.4
```

## Load the libraries

```r
library(nycflights13)
```

```
## Warning: package 'nycflights13' was built under R version 4.0.3
```

```r
library(tidyverse)
```

## nycflights13

```r
flights
```

```
## # A tibble: 336,776 x 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1      517            515         2      830            819
##  2  2013     1     1      533            529         4      850            830
##  3  2013     1     1      542            540         2      923            850
##  4  2013     1     1      544            545        -1     1004           1022
##  5  2013     1     1      554            600        -6      812            837
##  6  2013     1     1      554            558        -4      740            728
##  7  2013     1     1      555            600        -5      913            854
##  8  2013     1     1      557            600        -3      709            723
##  9  2013     1     1      557            600        -3      838            846
## 10  2013     1     1      558            600        -2      753            745
## # ... with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>
```

## Filter
Flights between JFK and SFO airports.

```r
flights %>% 
  filter(origin=="JFK" & dest=="SFO")
```

```
## # A tibble: 8,204 x 19
##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
##  1  2013     1     1      611            600        11      945            931
##  2  2013     1     1      655            700        -5     1037           1045
##  3  2013     1     1      729            730        -1     1049           1115
##  4  2013     1     1      734            737        -3     1047           1113
##  5  2013     1     1      745            745         0     1135           1125
##  6  2013     1     1      803            800         3     1132           1144
##  7  2013     1     1     1029           1030        -1     1427           1355
##  8  2013     1     1     1031           1030         1     1353           1415
##  9  2013     1     1     1112           1100        12     1440           1438
## 10  2013     1     1     1124           1100        24     1435           1431
## # ... with 8,194 more rows, and 11 more variables: arr_delay <dbl>,
## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>
```

##Plot
Count of flights between JFK and SFO airports by carrier.

```r
flights %>% 
  filter(origin=="JFK" & dest=="SFO") %>% 
  ggplot(aes(x=carrier))+
  geom_bar()
```

![](dummy_push_files/figure-html/unnamed-chunk-8-1.png)<!-- -->
