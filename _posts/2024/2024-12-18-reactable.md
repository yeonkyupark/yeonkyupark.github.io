---
title: reactable 패키지를 이용한 집계 표 만들기
date: 2024-12-18
categories: interest
tags: 
  - r
  - shiny
image: /assets/images/logo_R.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

## reactable 패키지를 이용한 집계 표 만들기

R에서 데이터를 정재, 집계한 후 표를 만들 때가 있다. `reactable` 패키지를 이용하면 보다 가독성이 좋은 표를 만들 수 있다.

```r
library(shiny)
library(reactable)

ui <- fluidPage(
  reactableOutput("table")
)

server <- function(input, output) {
  output$table <- renderReactable({
    reactable(
      mtcars[, c(1,2,7,11)],
      groupBy = "cyl",
      columns = list(
        mpg = colDef(aggregate = "mean", name="MPG(average)", format = colFormat(digits = 1)),
        qsec = colDef(aggregate = JS("function(values, rows) {return values[0]}"), name = "1/4 mile time(1st value)"),
        carb = colDef(aggregate = "unique", name = "Carburetors(Unique values)")
      )
    )
  })
}

shinyApp(ui, server)
```

![](/assets/images/2024-12-18-reactable_01.png)

위 예제는 mpg 컬럼에 대한 평균을, qsec 컬럼에 대한 첫 번째 값을, carb 컬럼에 대한 유일값을 각각 표시한다.


## 참고자료

1. [https://glin.github.io/reactable/index.html](https://glin.github.io/reactable/index.html)

