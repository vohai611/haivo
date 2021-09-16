---
title: An R package to retrieve Vietnam stock data
author: Hai Vo
date: '2021-08-06'
slug: []
categories: []
tags: [stock]

---


## Why
It is convenience to retrieve stock data to R because there are multiple package in R allow you to analyzing and run ML with time series such as `{modeltime}` `{fable}`. The`{tidyquant}` package made it simple by let user get stock data in Yahoo Finance to R in the "tidy" format. However, most of Vietnamese company does listed in Yahoo Finance, hence user must manual load the data into R before take advantage of other R packages.

This is my simple package that allow user to get the Vietnam stock data from cafef.vn and vndirect.com.vn. This package is the wrap around of `{httr}` package which send request to these two data source and parse the respond to R data frame (tibble). You can browse the package source code [here](https://github.com/vohai611/vnstockr)

## Install

To install this package, use:

```r
devtools::install_github("https://github.com/vohai611/vnstockr")
```

## Usage
This package only contain two function `get_cafeF()` and `get_vndirect()`. User just need to specify stock code (symbol) and time frame. For example:

```r
library(vnstockr)
acb <- get_vndirect('ACB', '1/1/2021', '1/12/2021')
acb
```

```
## # A tibble: 174 × 25
##    code  date       time    floor type  basicPrice ceilingPrice floorPrice  open
##    <chr> <date>     <chr>   <chr> <chr>      <dbl>        <dbl>      <dbl> <dbl>
##  1 ACB   2021-09-16 15:09:… HOSE  STOCK       31.2         33.4       29.0  31.2
##  2 ACB   2021-09-15 15:09:… HOSE  STOCK       31.5         33.7       29.3  31.5
##  3 ACB   2021-09-14 15:09:… HOSE  STOCK       31.9         34.1       29.7  31.8
##  4 ACB   2021-09-13 15:09:… HOSE  STOCK       32.3         34.6       30.0  32.3
##  5 ACB   2021-09-10 15:09:… HOSE  STOCK       32.4         34.7       30.2  32.5
##  6 ACB   2021-09-09 15:09:… HOSE  STOCK       32.2         34.4       29.9  32  
##  7 ACB   2021-09-08 15:09:… HOSE  STOCK       32.5         34.8       30.2  32.5
##  8 ACB   2021-09-07 15:09:… HOSE  STOCK       32.0         34.2       29.8  32.4
##  9 ACB   2021-09-06 15:09:… HOSE  STOCK       32           34.2       29.8  32.2
## 10 ACB   2021-09-01 15:09:… HOSE  STOCK       32           34.2       29.8  32  
## # … with 164 more rows, and 16 more variables: high <dbl>, low <dbl>,
## #   close <dbl>, average <dbl>, adOpen <dbl>, adHigh <dbl>, adLow <dbl>,
## #   adClose <dbl>, adAverage <dbl>, nmVolume <dbl>, nmValue <dbl>,
## #   ptVolume <dbl>, ptValue <dbl>, change <dbl>, adChange <dbl>,
## #   pctChange <dbl>
```

Data retrieve are in the same format as `{tidyquant}` package and could easily integrate with other R package quickly. For example, data could be visualized with `ggplot2`:


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


##  Note
`get_cafeF()` have to send multiple requests to cafef.vn, depend on the time frame user specified, therefore the speed is much slower compare with `get_vndirect()` which is only send one request.

<style type="text/css">
h2 {
  color: #9EBA89;
}
</style>
