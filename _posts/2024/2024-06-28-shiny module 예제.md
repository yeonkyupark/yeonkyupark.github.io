---
title: shiny module 예제
date: 2024-06-28
categories: interest
tags:
  - r
  - shiny
---
## ui, server 함수로 작성된 코드

```r
library(shiny)
library(timevis)

ui <- fluidPage(
  dateRangeInput("range", "", start = Sys.Date(), end = (Sys.Date() + 30)),
  timevisOutput("this_month"),
  timevisOutput("next_month")
)

server <- function(input, output, session) {
  range_month <- reactive({
    input$range
  })
  output$this_month <- renderTimevis({
    timevis() %>% 
      setWindow(range_month()[1], range_month()[2])
  })
  output$next_month <- renderTimevis({
    timevis() %>% 
      setWindow(range_month()[1]+30, range_month()[2]+30)
  })
}

shinyApp(ui, server)
```

## module로 구현한 코드

```R
library(shiny)
library(timevis)

daterange_UI <- function(id) {
  ns <- NS(id)
  tagList(
    dateRangeInput(ns("range"), "Range", start = "2024-06-01", end = "2024-06-30"),
    timevisOutput(ns("this_month")),
    timevisOutput(ns("next_month"))
  )
}

daterange_Server <- function(id, data) {
  moduleServer(
    id,
    function(input, output, session) {
      range <- reactive(input$range)
      output$this_month <- renderTimevis({
        timevis() %>% 
          setWindow(range()[1], range()[2])
      })
      output$next_month <- renderTimevis({
        timevis() %>%
          setWindow(range()[1]+30, range()[2]+30)
      })
    }
  )
}

ui <- fluidPage(
  daterange_UI("daterange")
)

server <- function(input, output, session) {
  daterange_Server("daterange", data = list(data1, data2))
}

shinyApp(ui = ui, server = server)
```

![실행화면](/assets/images/Pasted%20image%2020240628221335.png)

_\_EOF\__
