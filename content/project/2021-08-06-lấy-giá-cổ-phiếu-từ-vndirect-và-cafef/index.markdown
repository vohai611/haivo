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
acb <- get_vndirect('ACB', '1/5/2020', '1/5/2021')
acb |>
  head(5) |>
  knitr::kable()
```



|code |date       |time     |floor |type  | basicPrice| ceilingPrice| floorPrice| open|  high|   low| close| average| adOpen| adHigh| adLow| adClose| adAverage| nmVolume|      nmValue| ptVolume|     ptValue| change| adChange| pctChange|
|:----|:----------|:--------|:-----|:-----|----------:|------------:|----------:|----:|-----:|-----:|-----:|-------:|------:|------:|-----:|-------:|---------:|--------:|------------:|--------:|-----------:|------:|--------:|---------:|
|ACB  |2021-04-29 |15:04:05 |HOSE  |STOCK |       33.8|        36.15|      31.45| 33.8| 34.65| 33.60| 34.65|   34.27|  27.04|  27.72| 26.88|   27.72|    27.416| 16646300| 570480100000|  1654000| 57334200000|   0.85|     0.68|    2.5148|
|ACB  |2021-04-28 |15:04:02 |HOSE  |STOCK |       34.0|        36.35|      31.65| 33.5| 34.30| 33.40| 33.80|   33.82|  26.80|  27.44| 26.72|   27.04|    27.056|  5675200| 191953980000|   670000| 23630000000|  -0.20|    -0.16|   -0.5882|
|ACB  |2021-04-27 |15:04:02 |HOSE  |STOCK |       33.3|        35.60|      31.00| 33.0| 34.00| 32.65| 34.00|   33.37|  26.40|  27.20| 26.12|   27.20|    26.696|  6393000| 213347290000|   149000|  5110700000|   0.70|     0.56|    2.1021|
|ACB  |2021-04-26 |15:04:04 |HOSE  |STOCK |       33.4|        35.70|      31.10| 33.4| 33.40| 32.60| 33.30|   32.91|  26.72|  26.72| 26.08|   26.64|    26.328|  7119100| 234311370000|        0|           0|  -0.10|    -0.08|   -0.2994|
|ACB  |2021-04-23 |15:04:04 |HOSE  |STOCK |       32.5|        34.75|      30.25| 32.4| 33.45| 32.10| 33.40|   32.81|  25.92|  26.76| 25.68|   26.72|    26.248|  6687700| 219451575000|   286800|  9941300000|   0.90|     0.72|    2.7692|

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

