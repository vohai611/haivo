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
acb <- get_vndirect('ACB', '1/1/2021', '1/12/2021')
acb
```

```
## # A tibble: 170 × 25
##    code  date       time    floor type  basicPrice ceilingPrice floorPrice  open
##    <chr> <date>     <chr>   <chr> <chr>      <dbl>        <dbl>      <dbl> <dbl>
##  1 ACB   2021-09-10 15:09:… HOSE  STOCK       32.4         34.7       30.2  32.5
##  2 ACB   2021-09-09 15:09:… HOSE  STOCK       32.2         34.4       29.9  32  
##  3 ACB   2021-09-08 15:09:… HOSE  STOCK       32.5         34.8       30.2  32.5
##  4 ACB   2021-09-07 15:09:… HOSE  STOCK       32.0         34.2       29.8  32.4
##  5 ACB   2021-09-06 15:09:… HOSE  STOCK       32           34.2       29.8  32.2
##  6 ACB   2021-09-01 15:09:… HOSE  STOCK       32           34.2       29.8  32  
##  7 ACB   2021-08-31 15:08:… HOSE  STOCK       32.2         34.4       29.9  32.5
##  8 ACB   2021-08-30 15:08:… HOSE  STOCK       31.8         34.0       29.6  31.8
##  9 ACB   2021-08-27 15:08:… HOSE  STOCK       32.0         34.2       29.8  31.7
## 10 ACB   2021-08-26 15:08:… HOSE  STOCK       32.4         34.7       30.2  32.6
## # … with 160 more rows, and 16 more variables: high <dbl>, low <dbl>,
## #   close <dbl>, average <dbl>, adOpen <dbl>, adHigh <dbl>, adLow <dbl>,
## #   adClose <dbl>, adAverage <dbl>, nmVolume <dbl>, nmValue <dbl>,
## #   ptVolume <dbl>, ptValue <dbl>, change <dbl>, adChange <dbl>,
## #   pctChange <dbl>
```

Data could be visualized with `ggplot2`:


```r
library(ggplot2)
acb |>
  ggplot(aes(date, close))+
  geom_line()+
  scale_x_date(date_breaks = "4 weeks")+
  theme_light()+
  theme(axis.text.x = element_text(angle = 45, hjust =1))+
  labs(x = NULL)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />


# Note
`get_cafeF()` have to send multiple POST requests to cafef.vn, hence the speed is much slower than `get_vndirect()` which is only send one request. It also have higher chance of break in the future.



