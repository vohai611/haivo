---
title: test Rmarkdown format
author: Hai Vo
date: '2021-08-01'
slug: []
categories: []
tags: []
---

## Hello


```r
library(ggplot2)
```

```
## Warning: package 'ggplot2' was built under R version 4.0.2
```

```r
library(magrittr)
```

```
## Warning: package 'magrittr' was built under R version 4.0.2
```

```r
mtcars %>% 
  ggplot(aes(mpg, cyl))+
  geom_point()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />


## World
