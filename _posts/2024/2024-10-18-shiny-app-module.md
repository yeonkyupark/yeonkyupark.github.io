---
title: shiny app 모듈 구조
date: 2024-10-18
categories: Interest
tags:
  - shiny
  - R
image: /assets/images/logo_R.png
toc: true
pin: false
math: true
mermaid: true
description: shiny app을 모듈화 하기 위한 구조를 알아 본다.
---

## shiny module

```r
nameUI <- function(id) {
  ns <- NS(id)
  tagList(
  
  )
}

nameServer <- function(id) {
  moduleServer(
    id,
    function(input, output, session) {
      
    }
  )
}
```

## Reference
