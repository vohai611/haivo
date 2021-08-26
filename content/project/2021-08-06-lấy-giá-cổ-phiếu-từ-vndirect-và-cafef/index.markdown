---
title: An R package to retrieve Vietnam stock data
author: Hai Vo
date: '2021-08-06'
slug: []
categories: []
tags: [stock]
---


This is my simple package that allow user to get the Vietnam stock data from cafef.vn and vndirect. This package is the wrap around of `httr` package to send request to these two data source and parse the respond to R data frame (tibble). You can browse the package source code [here](https://github.com/vohai611/vnstockr)

# Install

To install this package, use:

```r
devtools::install_github("https://github.com/vohai611/vnstockr")
```

# Usage
This package only contain two function `get_cafeF()` and `get_vndirect()`. User just need to specify stock code (symbol) and time frame. For example:

```r
library(vnstockr)
get_vndirect('ACB', '1/1/2021', '1/12/2021')
```

```
## # A tibble: 147 × 25
##    code  date       time    floor type  basicPrice ceilingPrice floorPrice  open
##    <chr> <date>     <chr>   <chr> <chr>      <dbl>        <dbl>      <dbl> <dbl>
##  1 ACB   2021-08-06 15:08:… HOSE  STOCK       36           38.5       33.5  36.1
##  2 ACB   2021-08-05 15:08:… HOSE  STOCK       35.5         38.0       33.0  35.4
##  3 ACB   2021-08-04 15:08:… HOSE  STOCK       35.8         38.3       33.3  36  
##  4 ACB   2021-08-03 15:08:… HOSE  STOCK       35.6         38         33.1  35.4
##  5 ACB   2021-08-02 15:08:… HOSE  STOCK       36.2         38.6       33.6  35.5
##  6 ACB   2021-07-30 15:07:… HOSE  STOCK       34.2         36.5       31.8  34.3
##  7 ACB   2021-07-29 15:07:… HOSE  STOCK       33.2         35.4       30.8  33.4
##  8 ACB   2021-07-28 15:07:… HOSE  STOCK       33.2         35.4       30.8  33.2
##  9 ACB   2021-07-27 15:07:… HOSE  STOCK       32.7         35.0       30.4  33.0
## 10 ACB   2021-07-26 15:07:… HOSE  STOCK       33           35.3       30.7  32.6
## # … with 137 more rows, and 16 more variables: high <dbl>, low <dbl>,
## #   close <dbl>, average <dbl>, adOpen <dbl>, adHigh <dbl>, adLow <dbl>,
## #   adClose <dbl>, adAverage <dbl>, nmVolume <dbl>, nmValue <dbl>,
## #   ptVolume <dbl>, ptValue <dbl>, change <dbl>, adChange <dbl>,
## #   pctChange <dbl>
```

# Note
`get_cafeF()` have to send multiple POST requests to cafef.vn, hence the speed is much slower than `get_vndirect()` which is only send one request. It also have higher chance of break in the future.



