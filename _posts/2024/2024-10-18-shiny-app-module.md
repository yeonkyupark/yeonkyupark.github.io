---
title: shiny app 모듈 구조
date: 2024-10-18
categories: interest
tags:
  - shiny
  - r
image: /assets/images/logo_R.png
toc: true
pin: false
math: true
mermaid: true
description: shiny app을 모듈화 하기 위한 구조를 알아 본다.
---

## shiny module

shiny module 기본 구조는 아래와 같다. module로 구성하기 이전에 ui 코드는 nameUI에, server 코드는 nameServer에 작성한다. nameUI에서는 ui에서 넘어오는 객체는 인식하기 위해 namespace로 감싼다.

```r
nameUI <- function(id) {
  ns <- NS(id)
  tagList(
    # ui code
  )
}

nameServer <- function(id) {
  moduleServer(
    id,
    function(input, output, session) {
      # server code
    }
  )
}
```

## module 작성

### 기존 코드

데이터셋에서 x축과 y축을 지정하면 산포도를 그려주는 app 코드이다[^1].

[^1]: [https://www.youtube.com/watch?v=BufC0agHnzw](https://www.youtube.com/watch?v=BufC0agHnzw)

```r
library(shiny)
library(ggplot2)


ui <- fluidPage(
  theme =  bslib::bs_theme(bootswatch = 'flatly'),
  tabsetPanel(
    tabPanel("Penguins", {
      sidebarLayout(
        sidebarPanel(
          selectInput(
            'select_var_1_penguins',
            'Variable 1',
            choices = names(palmerpenguins::penguins)
          ),
          selectInput(
            'select_var_2_penguins',
            'Variable 2',
            choices = names(palmerpenguins::penguins)
          ),
          actionButton(
            'draw_scatterplot_penguins',
            'Draw scatterplot',
          )
        ),
        mainPanel(
          plotOutput('scatterplot_penguins')
        )
      )
    }),
    tabPanel("Iris", {
      sidebarLayout(
        sidebarPanel(
          selectInput(
            'select_var_1_iris',
            'Variable 1',
            choices = names(iris)
          ),
          selectInput(
            'select_var_2_iris',
            'Variable 2',
            choices = names(iris)
          ),
          actionButton(
            'draw_scatterplot_iris',
            'Draw scatterplot',
          )
        ),
        mainPanel(
          plotOutput('scatterplot_iris')
        )
      )
    })
  )
)

server <- function(input, output, session) {
  
  output$scatterplot_penguins <- renderPlot({
    ggplot(palmerpenguins::penguins) +
      geom_point(
        aes_string(input$select_var_1_penguins, input$select_var_2_penguins), 
        size = 3,
        alpha = 0.5,
        col = 'dodgerblue4'
      )
  }) |> bindEvent(input$draw_scatterplot_penguins)
  
  output$scatterplot_iris <- renderPlot({
    ggplot(iris) +
      geom_point(
        aes_string(input$select_var_1_iris, input$select_var_2_iris), 
        size = 3,
        alpha = 0.5,
        col = 'dodgerblue4'
      )
  }) |> bindEvent(input$draw_scatterplot_iris)
  
  
}

shinyApp(ui, server)
```

![](/assets/images/2024-10-18-shiny-app.png)

ui/server에 작성된 코드를 보면 데이터셋만 다를 뿐 화면구성과 서버단에서 처리하는 동작은 동일하다. 따라서 데이터셋에 따라 동작하도록 모듈로 구성하면 코드를 단순화할 수 있다.

## 모듈 코드

### 1단계 - 모듈 작성

ui와 server 코드를 각 모듈 함수로 이동시킨다.

```r
library(shiny)
library(ggplot2)


plot_UI <- function(id, dataset) {
  ns <- NS(id)
  tagList(
    sidebarLayout(
      sidebarPanel(
        selectInput(
          ns('select_var_1_penguins'),
          'Variable 1',
          choices = names(dataset)
        ),
        selectInput(
          ns('select_var_2_penguins'),
          'Variable 2',
          choices = names(dataset)
        ),
        actionButton(
          ns('draw_scatterplot_penguins'),
          'Draw scatterplot',
        )
      ),
      mainPanel(
        plotOutput(ns('scatterplot_penguins'))
      )
    )
  )
}

plot_Server <- function(id, dataset) {
  moduleServer(
    id,
    function(input, output, session) {
      output$scatterplot_penguins <- renderPlot({
        ggplot(dataset) +
          geom_point(
            aes_string(input$select_var_1_penguins, input$select_var_2_penguins), 
            size = 3,
            alpha = 0.5,
            col = 'dodgerblue4'
          )
      }) |> bindEvent(input$draw_scatterplot_penguins)
    }
  )
}

ui <- fluidPage(
  theme =  bslib::bs_theme(bootswatch = 'flatly'),
  tabsetPanel(
    tabPanel("Penguins", {
      # move to plot_UI
    }),
    tabPanel("Iris", {
      # move to plot_UI
    })
  )
)

server <- function(input, output, session) {
	# move to plot_Server
}

shinyApp(ui, server)
```

### 2단계 - 모듈 함수 호출

모듈로 작성된 함수를 ui/server에서 적절하게 호출한다.

```r
library(shiny)
library(ggplot2)


plot_UI <- function(id, dataset) {
  ns <- NS(id)
  tagList(
    sidebarLayout(
      sidebarPanel(
        selectInput(
          ns('select_var_1_penguins'),
          'Variable 1',
          choices = names(dataset)
        ),
        selectInput(
          ns('select_var_2_penguins'),
          'Variable 2',
          choices = names(dataset)
        ),
        actionButton(
          ns('draw_scatterplot_penguins'),
          'Draw scatterplot',
        )
      ),
      mainPanel(
        plotOutput(ns('scatterplot_penguins'))
      )
    )
  )
}

plot_Server <- function(id, dataset) {
  moduleServer(
    id,
    function(input, output, session) {
      output$scatterplot_penguins <- renderPlot({
        ggplot(dataset) +
          geom_point(
            aes_string(input$select_var_1_penguins, input$select_var_2_penguins), 
            size = 3,
            alpha = 0.5,
            col = 'dodgerblue4'
          )
      }) |> bindEvent(input$draw_scatterplot_penguins)
    }
  )
}

ui <- fluidPage(
  theme =  bslib::bs_theme(bootswatch = 'flatly'),
  tabsetPanel(
    tabPanel("Penguins", {
      plot_UI('Penguins', palmerpenguins::penguins) # call module
    }),
    tabPanel("Iris", {
      plot_UI('Iris', iris) # call module
    })
  )
)

server <- function(input, output, session) {
  plot_Server('Penguins', palmerpenguins::penguins) # call module
  plot_Server('Iris', iris) # call module
} 

shinyApp(ui, server)
```

추가된 데이터셋에 동일한 구조로 화면을 구성한다면 다음과 같이 쉽게 코드를 완성할 수 있다.

```r
ui <- fluidPage(
  theme =  bslib::bs_theme(bootswatch = 'flatly'),
  tabsetPanel(
    tabPanel("Penguins", {
      plot_UI('Penguins', palmerpenguins::penguins)
    }),
    tabPanel("Iris", {
      plot_UI('Iris', iris)
    }),
    # add cars dataset _________________________________
    tabPanel("Cars", { 
      plot_UI('Cars', cars)
    })
  )
)

server <- function(input, output, session) {
  plot_Server('Penguins', palmerpenguins::penguins)
  plot_Server('Iris', iris)
  # add cars dataset _________________________________
  plot_Server('Cars', cars) 
}
```

## Reference
