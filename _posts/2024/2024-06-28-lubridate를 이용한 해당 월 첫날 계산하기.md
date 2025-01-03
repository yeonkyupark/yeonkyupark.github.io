---
title: lubridate를 이용한 해당 월 첫날 계산하기
date: 2024-06-28
categories: interest
tags:
  - r
  - lubridate
---
## Basic

```r
today <- Sys.Date()
first_day_of_month <- today - (as.integer(substr(today, 9, 10)) - 1)
```

```r
c(today, first_day_of_month)
```

```
## [1] "2024-06-28" "2024-06-01"
```

```r
today <- as.Date("2024-12-31")
today + 2
```

```
## [1] "2025-01-02"
```

## lubridate package

### 그 달 첫 날

`floor_date()` 함수는 `unit` 단위에 맞춰 내림을 한다. unit이 `month`인 경우 그 달 첫 날을 의미하게 된다.

```r
floor_date(today(), unit = "month")
```

```
## [1] "2024-06-01"
```

### 그 달 막 날

`ceiling_date()` 함수는 `unit` 단위에 맞춰 올올림을 한다. unit이 `month`인 경우 그 다음 첫 날을 의미하게 된다. 따라서 그 달 마지막 날을 계산하기 위해서는 하루를 빼 주면 된다.

```r
ceiling_date(today(), unit = "month") - 1
```

```
## [1] "2024-06-30"
```

```r
last_day_of_this_year <- ceiling_date(as.Date("2024-12-30"), unit = "month") - 1
first_day_of_next_year <- ceiling_date(as.Date("2024-12-30"), unit = "month")
```

```r
c(last_day_of_this_year, first_day_of_next_year)
```

```
## [1] "2024-12-31" "2025-01-01"
```


_\_EOF\__
