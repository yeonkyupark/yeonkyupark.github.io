---
title: Shiny get started
date: 2024-06-23
categories: interest
tags:
  - r
  - shiny
---
## Shiny Package
![](https://shiny.posit.co/images/shiny-solo.png)

Shiny는 대화형 웹 어플리케이션 개발을 위한 R 언어 패키지이다.

```r
install.packages("shiny")
library(shiny)
runExample("01_hello")
```

![](https://shiny.posit.co/r/getstarted/shiny-basics/lesson1/images/01_hello.png)
### runExample()
패키지를 설치하면 `runExample()` 함수로 간단한 예제를 살펴 볼 수 있다. `[Package _shiny_ version 1.8.1.1` 기준 11개 예제를 제공한다.

```r
runExample("01_hello")      # a histogram
runExample("02_text")       # tables and data frames
runExample("03_reactivity") # a reactive expression
runExample("04_mpg")        # global variables
runExample("05_sliders")    # slider bars
runExample("06_tabsets")    # tabbed panels
runExample("07_widgets")    # help text and submit buttons
runExample("08_html")       # Shiny app built from HTML
runExample("09_upload")     # file upload wizard
runExample("10_download")   # file download wizard
runExample("11_timer")      # an automated timer
```

## Shiny app 구조
Shiny app은 `app.R` 파일 하나로 구성되며, `runApp()` 함수에 app.R 파일을 포함된 디렉토리 명을 인자로 주어 실행한다. app.R 파일은 아래 3가지로 구성된다.
- User Infterface
- Server function
- shinyApp 호출 함수

```r
library(shiny)

# See above for the definitions of ui and server
ui <- ...                           # user interface

server <- ...                       # server function

shinyApp(ui = ui, server = server)  # call shinyapp
```

app.R 파일을 작성 한 후 `my_app` 디렉토리에 저장했다면 다음과 같이 실행할 수 있다.
```r
library(shiny)
runApp("my_app")
```

Rstudio 사용 시 `Run App` 버튼이나 `Ctrl + Shift + Enter`로 Shiny App 실행이 가능하다.
![](https://shiny.posit.co/r/getstarted/shiny-basics/lesson1/images/run-app.png)

> **참고자료**
>  - https://shiny.posit.co/r/getstarted/shiny-basics/lesson1/index.html
>  - https://mastering-shiny.org/index.html
{: .prompt-tip }
