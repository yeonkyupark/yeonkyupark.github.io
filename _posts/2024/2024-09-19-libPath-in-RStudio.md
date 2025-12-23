---
title: RStudio에서 libPath를 설정하자
date: 2024-09-19
categories: interest
tags:
  - r
  - rstudio
---
## RStudio에서 R package 설치 경로 확인
R에서는 다양한 패키지를 제공하고 있다. 패키지는 버전에 따라 설치되는 경로가 다를 수 있다. 즉 R 버전이 다양하면 다양한 버전만큼 패키지를 다운로드하여 자신 PC에 설치를 하게 된다. 참고라 현 시점 R 버전은 4.4.1이고 lib를 설치하는 기본 경로는 다음과 같다.

```{r}
> .libPaths()
[1] "C:/Program Files/R/R-4.4.1/library"
```


## 사용자 정의 libPath 지정
R 패키지 설치 경로를 지정하고 싶다면 다음과 같이 진행하다.

1. 시스템 환경 변수 설정
   ![](/assets/images/Pasted%20image%2020240919230557.png)
2. RStudio 재시작(실행 중인 경우)
3. “.libPaths()” 함수를 통해 변경된 경로 확인
```{r}
> .libPaths()
[1] "D:/R/library"                       "C:/Program Files/R/R-4.4.1/library"
```

_\_EOF\__
