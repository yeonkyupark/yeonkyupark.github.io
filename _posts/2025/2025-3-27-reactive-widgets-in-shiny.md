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
Group2|D
Group2|X
Group2|Y
Group2|Z

`selectInput1` widget에서 `Group2`을 선택하면 `selectInput2`에서는 "X, Y, Z"만 출력되도록 한다.

## 구현

### Layout 구성

### reactive 등록

`selectInput1` 변경을 인식하기 위해 reactive로 등록한다. 선택값에 따라 출력할 목록을 지정해 준다.

### 변경사항 반영
`observe()` 함수를 통해 변경사항이 발생하면 `updateSelectInput()` 함수로 변경된 내용을 반영한다.

## 참고사항



