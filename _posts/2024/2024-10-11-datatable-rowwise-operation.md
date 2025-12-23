---
title: data.table 행별로 연산하기
date: 2024-10-11
categories: interest
tags:
  - r
  - data.table
---

## data.table에서 행 단위로 연산하기

대부분 데이터는 엑셀과 같이 행과 열로 구성 되어있다. 이런 형태를 R에서는 matrix, list, data.frame, data.tibble, data.table 자료형으로 처리한다. 이렇게 구성된 자료 형태는 일반적으로열 단위로 연산이 이루어진다. 데이터 분석을 하다 보면 자료 특성에 따라 행 단위로 연산이 필요한 경우가 있다.

다음은 data.table자료형에서 행 단위로 연산을 하는 예제이다.

```r
library(data.table)
data <- data.table(
x = c(1,2,3,4,5),
y = c(5,4,3,2,1),
z = c(1,0,1,0,1)
)

data[, row_sum := apply(data, 1, sum)]

data
```

_\_EOF\__
