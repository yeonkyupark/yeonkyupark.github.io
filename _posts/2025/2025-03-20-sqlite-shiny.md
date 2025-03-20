---
title: SQLite와 Shiny 연동하기 
date: 2025-03-20
categories: hobby
tags: [sqlite, shiny]
image: /assets/images/logo_sqlite.png
toc: true
pin: false
math: true
mermaid: true
description: shiny에서 sqlite를 사용하기 위해 필요한 패키지를 알아보고 테이블을 읽어 화면에 출력하는 기능을 구현한다.
keywords: ["r", "shiny"]
---

## SQLite와 Shiny 연동하기

### SQLite package 설치

Shiny에서 SQLite를 사용하기 위해서는 `SQLite`, `pool` `DBI` 패키지를 설치한다.

```r
install.packages("RSQLite")
install.packages("pool")
install.packages("DBI")
```

db connection은 pool 패키지를 이용하고, table 쿼리는 DBI를 이용한다. 참고로 두 패키지를 비교하면 다음과 같다.

|항목|DBI 패키지|pool 패키지|
|---|---|---|
|**주요 기능**|데이터베이스 연결 및 쿼리 실행|데이터베이스 연결 풀링 제공|
|**특징**|- R에서 DB를 직접 연결하고 쿼리 실행<br>- SQLite, MySQL 등 다양한 DB 드라이버와 함께 사용|- DBI 기반으로 커넥션 풀 제공<br>- 여러 사용자가 동시에 앱 사용 시 효율적인 커넥션 관리 가능|
|**적합한 상황**|- 단순한 앱<br>- 사용자 수가 적은 환경|- 사용자 수가 많은 앱<br>- 동시 접속자가 많은 환경|
|**연결 관리**|매 쿼리 실행 시마다 `dbConnect()` / `dbDisconnect()` 사용|자동으로 커넥션 풀에서 커넥션 할당 및 반환|
|**코드 복잡성**|상대적으로 단순|상대적으로 복잡 (초기 설정 필요)|
|**성능**|소규모 앱에서 충분|대규모 앱에서 더 나은 성능|

### pool 생성 및 종료

파일 구조는 `global.R`, `server.R`, `ui.R`로 나눠서 구성하고 `pool` 생성은 `global.R`에 종료는 `server.R`에 작성한다.

```r
# globa.R

db_name <- config::get()$db$db_name
pool <- pool::dbPool(RSQLite::SQLite(), dbname = db_name)
```

```r
# server.R

server <- function(input, output, session) {
  
  # 앱 종료 시 pool 닫기
  onStop(function() {
    pool::poolClose(pool)
  })

  ...
```

### 테이블 읽어 오기

필요한 테이블은 `dbReadTable` 함수로 읽어 온다.

```r
server <- function(input, output, session) {
  
  ...
  
  rv <- reactiveValues()
  
  data_kdt_east <- reactive({
    data <- dbReadTable(pool, tbl_kdt_east)
  })
...
```

### 테이블 처리

읽어 온 테이블을 적절히 처리한다. 본 예제에서는 DT 패키지를 이용하여 화면에 출력하는 예제를 작성한다. 테이블 내용은 해파랑길 코스 정보이다.[^1]

```r
kdt_UI <- function(id) {
  ns <- NS(id)
  tagList(
    DTOutput(ns(id))
  )
}

kdt_Server <- function(id, dataset) {
  moduleServer(
    id,
    function(input, output, session) {
      output[[id]] <- renderDT({
        kdt_data <- dataset()
        colnames(kdt_data) <- kdt_east_colnames
        kdt_data
        })
    }
  )
}
```

### 화면 출력

![](/assets/images/2025-03-20-sqlite-shiny.png) 

_[live demo](https://yeonkyupark.shinyapps.io/Grain-Data-Shiny-Demo/)_


## 참고자료
1. [R shiny와 DB를 동기화 해보자(Sqlite)](https://unfinishedgod.netlify.app/2020/08/23/r-shiny%EC%99%80-db%EB%A5%BC-%EB%8F%99%EA%B8%B0%ED%99%94-%ED%95%B4%EB%B3%B4%EC%9E%90sqlite/)
2. [Using pool with dplyr](https://rstudio.github.io/pool/articles/pool-dplyr.html)
3. [Using the pool package (advanced)](https://shiny.posit.co/r/articles/build/pool-advanced/)

**각주**

[^1]: https://www.durunubi.kr/koreatrail-introduction.do
