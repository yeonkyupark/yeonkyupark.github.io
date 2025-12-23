---
title: 그룹별 결측치 처리하기 
date: 2025-01-06
categories: interest
tags: 
  - r
  - data.table
  - dplyr
image: /assets/images/logo_wrangling.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

## 그룹별(범주별) 결측치 처리하기

결측치를 처리하는 방법은 다양하다. 그 중 하나가 평균값으로 대체하는 방법이 있다. 하지만 데이터가 범주를 갖는다면 전체 평균값을 대체하는 방식보다 각 범주별로 평균값을 계산하여 반영하는 편이 보다 정확한 분석이 가능하다. 아래 예제를 통해 그룹(범주)별 평균값으로 대체하는 방법을 알아본다.

```r
library(dplyr)
library(data.table)

# 예시 데이터프레임 생성
df <- data.table(
  group = c('A', 'A', 'B', 'B', 'C', 'C', 'C'),
  value1 = c(1, NA, 3, 4, NA, 6, 7),
  value2 = c(1, NA, 3, NA, 5, 6, 7),
  value3 = c(1, 2, 3, 4, NA, NA, 7)
)
```

```
> df
    group value1 value2 value3
   <char>  <num>  <num>  <num>
1:      A      1      1      1
2:      A     NA     NA      2
3:      B      3      3      3
4:      B      4     NA      4
5:      C     NA      5     NA
6:      C      6      6     NA
7:      C      7      7      7
```

### dplyr 패키지를 이용한 경우

```r
df %>%
  group_by(group) %>% 
  mutate(across(value1:value3, ~ifelse(is.na(.), mean(., na.rm=T), .)))
```

```
# A tibble: 7 × 4
# Groups:   group [3]
  group value1 value2 value3
  <chr>  <dbl>  <dbl>  <dbl>
1 A        1        1      1
2 A        1        1      2
3 B        3        3      3
4 B        4        3      4
5 C        6.5      5      7
6 C        6        6      7
7 C        7        7      7
```

### data.table 패키지를 이용한 경우

```r
cols <- colnames(df)[colnames(df) != "group"]
for(col in cols) {
  df[, (col) := ifelse(is.na(df[[col]]), 
                       ave(df[[col]], group, FUN=function(x) mean(x, na.rm=T)),
                       df[[col]])]
}
df
```

```
    group value1 value2 value3
   <char>  <num>  <num>  <num>
1:      A    1.0      1      1
2:      A    1.0      1      2
3:      B    3.0      3      3
4:      B    4.0      3      4
5:      C    6.5      5      7
6:      C    6.0      6      7
7:      C    7.0      7      7
```

## 참고자료

