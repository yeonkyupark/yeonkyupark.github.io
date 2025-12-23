---
title: "제목 영역없이 그래프 그리기"
date: "2025-03-06" 
categories: [interest]
tags: [r]
image: /assets/images/logo_r.png
toc: true
pin: false
math: true
mermaid: true
description: R, plot, title 영역없이 그래프 그리기
---

## 제목 영역없이 그래프 그리기

R에서 그래프를 그릴 때, 제목 영역이 필요가 없을 수 있다. 이 때 단순히 제목(main) 옵션만 생략하면 제목 자체만 출력되지 않을 뿐 제목 영역은 그대로 남아 있게 된다. 이 영역을 삭제하기(줄이기) 위해서는 아래와 같이 코드를 작성한다.

```r
par(mar=c(5,3,2,2)+0.1)
hist(rnorm(100),ylab=NULL,main=NULL)
dev.off()
```

`par()` 함수는 그래픽 설정을 변경하는 함수로 `mar`(margin, 여백) 옵션을 통해 상단 부분을 줄일 수 있다.

위 코드는 다음과 같이 동작하게된다.

| 방향   | 기본 설정 값 | `+0.1` 적용 후 |
|--------|------------|---------------|
| 아래(bottom) | 5          | 5.1           |
| 왼쪽(left)   | 3          | 3.1           |
| 위(top)      | 2          | 2.1           |
| 오른쪽(right) | 2          | 2.1           |

참고로 `mar` 옵션 기본값은 다음과 같다.

```
mar=c(5,4,4,2)+0.1 # c(bottom, left, top, right) 
```

![](assets/images/plot_without_title.png)

## 참고자료

1. [Plots without titles/labels in R](https://stackoverflow.com/questions/736541/plots-without-titles-labels-in-r)



