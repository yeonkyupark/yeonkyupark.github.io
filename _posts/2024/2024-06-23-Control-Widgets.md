---
title: Control Widgets
date: 2024-06-23
categories: interest
tags:
  - r
  - shiny
---
## 기본 Widgets
![](https://shiny.posit.co/r/getstarted/shiny-basics/lesson3/images/basic-widgets.png)

| function           | widget                                         |
|--------------------|------------------------------------------------|
| actionButton       | Action Button                                  |
| checkboxGroupInput | A group of check boxes                         |
| checkboxInput      | A single check box                             |
| dateInput          | A calendar to aid date selection               |
| dateRangeInput     | A pair of calendars for selecting a date range |
| fileInput          | A file upload control wizard                   |
| helpText           | Help text that can be added to an input form   |
| numericInput       | A field to enter numbers                       |
| radioButtons       | A set of radio buttons                         |
| selectInput        | A box with choices to select from              |
| sliderInput        | A slider bar                                   |
| submitButton       | A submit button                                |
| textInput          | A field to enter text                          |

각 widget 함수 기본 형태는 다음과 같다.
```r
actionButton(inputId, label, icon = NULL, width = NULL, disabled = FALSE, ...)
```
- inputID - server function에서 참조할 이름(widget 이름)
- label - widget에 표시할 이름
- 그 외 함수에 따른 옵션
### Widget 예시
![](/assets/images/Pasted%20image%2020240623165141.png)

```R
library(shiny)

# Define UI ----
ui <- page_fluid(
  titlePanel("Basic widgets"),
  layout_columns(
    col_width = 3,
    card(
      card_header("Buttons"),
      actionButton("action", "Action"),
      submitButton("Submit")
    ),
    card(
      card_header("Single checkbox"),
      checkboxInput("checkbox", "Choice A", value = TRUE)
    ),
    card(
      card_header("Checkbox group"),
      checkboxGroupInput(
        "checkGroup",
        "Select all that apply",
        choices = list("Choice 1" = 1, "Choice 2" = 2, "Choice 3" = 3),
        selected = 1
      )
    ),
    card(
      card_header("Date input"),
      dateInput("date", "Select date", value = "2014-01-01")
    ),
    card(
      card_header("Date range input"),
      dateRangeInput("dates", "Select dates")
    ),
    card(
      card_header("File input"),
      fileInput("file", label = NULL)
    ),
    card(
      card_header("Help text"),
      helpText(
        "Note: help text isn't a true widget,",
        "but it provides an easy way to add text to",
        "accompany other widgets."
      )
    ),
    card(
      card_header("Numeric input"),
      numericInput("num", "Input number", value = 1)
    ),
    card(
      card_header("Radio buttons"),
      radioButtons(
        "radio",
        "Select option",
        choices = list("Choice 1" = 1, "Choice 2" = 2, "Choice 3" = 3),
        selected = 1
      )
    ),
    card(
      card_header("Select box"),
      selectInput(
        "select",
        "Select option",
        choices = list("Choice 1" = 1, "Choice 2" = 2, "Choice 3" = 3),
        selected = 1
      )
    ),
    card(
      card_header("Sliders"),
      sliderInput(
        "slider1",
        "Set value",
        min = 0,
        max = 100,
        value = 50
      ),
      sliderInput(
        "slider2",
        "Set value range",
        min = 0,
        max = 100,
        value = c(25, 75)
      )
    ),
    card(
      card_header("Text input"),
      textInput("text", label = NULL, value = "Enter text...")
    )
  )
)

# Define server logic ----
server <- function(input, output) {

}

# Run the app ----
shinyApp(ui = ui, server = server)
```

widget 관련 자세한 내용은 [Shiny Widgets Gallery](https://shiny.posit.co/gallery/widget-gallery.html) 참고 한다.

> 참고자료
> - [https://shiny.posit.co/r/getstarted/shiny-basics/lesson3/](https://shiny.posit.co/r/getstarted/shiny-basics/lesson3/)

_\_EOF\__