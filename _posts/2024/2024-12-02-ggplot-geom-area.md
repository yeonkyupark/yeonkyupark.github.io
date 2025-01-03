---
title: geom_area를 이용하여 정규분포를 표현해 보자
date: 2024-12-02
categories: interest
tags: 
  - ggplot
image: /assets/images/logo_ggplot.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

## geom_area를 이용하여 정규분포를 표현해 보자

```r
library(ggplot2)
df_norm <- data.frame(x = seq(-5, 5, 0.01),
                      density = dnorm(x = seq(-5, 5, 0.01), mean = 0, sd = 1))

ggplot(df_norm, aes (x = x, y = density)) +
    geom_path(color = "cornflowerblue", size = 1.2) +
    scale_x_continuous(expand = c(0, 0)) +
    scale_x_continuous(breaks = seq(-5,5,1)) + 
    geom_area(data = subset(df_norm, x <= qnorm(0.025) ), fill = 'cornflowerblue', alpha=.7) +
    geom_area(data = subset(df_norm, x >= qnorm(0.975) ), fill = 'cornflowerblue', alpha=.7) + 
    annotate("text", x = c(-2.3, 2.3), y = 0.01, label = c(0.025, 0.025)) +
    annotate("text", x = 0, y = dnorm(0)+0.01, label = round(dnorm(0),4)) + 
    theme_classic()
```

![](/assets/images/2024-12-02-ggplot-geom-area.png)
