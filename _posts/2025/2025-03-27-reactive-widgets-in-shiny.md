---
title: R Shiny Widget 변경시 다른 Widget도 변경해 보자
date: 2025-03-27 
categories: [hobby]
tags: [r, shiny]
image: /assets/images/logo_shiny.png
toc: true
pin: false
math: true
mermaid: true
description: shiny ui widget 변경 시 함께 연동되는 다른 widget도 함께 변경하는 방법을 알아본다.
---

## R Shiny Widget 변경시 연동된 Widget 함게 변경하기

Shiny Widget을 이용하여 UI를 구성할 때 계층적으로 배치하는 경우가 있다. 예를 들어 카테고리에 따른 상품명을 달리 표시한다거나 선택한 항목에 따라 범위 설정을 달리해야 하는 경우가 해당된다.

아래 표를 하면에 구성할 경우를 생각해 보자.

Group|Item
-|-
Group1|A
Group1|B
Group1|C
Group1|D
Group2|X
Group2|Y
Group2|Z


![](/assets/images/2025-3-27-reactive-widgets-in-shiny.png)

이제 `selectInput1` widget에서 `Group2`을 선택하면 `selectInput2`에서는 "X, Y, Z"만 출력되도록 한다.

## 구현

### Layout 구성

아래와 같이 간단하게 `secectInput` widget을 위아래로 배치한다.

```r
selectInput("selectInput1", "Select Group", 
            multiple = F, choices = c("Group1", "Group2")),
selectInput("selectInput2", "Select Item",
            multiple = F, choices = c("A", "B", "C", "D", "X", "Y", "Z")))
```

### reactive 등록

`selectInput1` 변경시 `selectInput2` 값을 설정하기 위해 reactive value를 등록한다. `get_items()`은 `selectInput1` 값을 읽어 적절한 `selectInput2`  값을 설정한다.

```r
  get_items <- reactive({
    req(input$selectInput1)
    if(input$selectInput1 == "Group1") {
      c("A", "B", "C", "D")
    } else if(input$selectInput1 == "Group2") {
      c("X", "Y", "Z")
    } else {
      c("A", "B", "C", "D", "X", "Y", "Z")
    }
  })

```

### 변경사항 반영
`observeEvent()` 함수를 통해 변경사항이 발생하면 `updateSelectInput()` 함수로 변경된 내용을 반영한다. `selectInput1`을 지켜보고 있다가 변경이 발생하면 `selectInput2` 값을 갱신한다. 이때 위에서 작성한 `get_items()`를 통해 적절한 값을 출력한다.

```r
  observeEvent(input$selectInput1, {
    updateSelectInput(session, inputId = "selectInput2", 
                      choices = get_items()
    )
  })
```

### 결과 확인

![](/assets/images/2025-3-27-reactive-widgets-in-shiny-1.png)

- [live demo](https://yeonkyupark.shinyapps.io/Grain-Data-Shiny-Demo/)

## 참고자료

1. [Observe Function in R Shiny - How to Implement a Reactive Observer](https://www.appsilon.com/post/observe-function-r-shiny)
2. [R Shiny - What is the problem with my observe function ({UpdateSelectInput})?](https://stackoverflow.com/questions/62293044/r-shiny-what-is-the-problem-with-my-observe-function-updateselectinput)

