---
title: "Quarto Book 실행 코드 출력물 스타일을 바꿔보자"
date: "2024-11-26"
categories: Hobby
tags: 
  - quarto
image: /assets/images/rstudio_log.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

## Quarto Book 실행 코드 출력물 스타일을 바꿔보자

style.css 파일에 아래와 같이 실행 코드 산출물 배경색을 정의 한다.
그리고 파일 상단에 `css: style.css`를 추가한다.

{% raw %}
```css
.styled-output .cell-output {
  background-color: silver;
  border-radius: 4px;
}
```
{% endraw %}

{% raw %}
```qmd
---
title: "Untitled"
format: html
css: style.css
---
```
{% endraw %}

## Reference

1. https://stackoverflow.com/questions/76610798/change-color-and-background-of-chunk-ouput-in-quarto-document
