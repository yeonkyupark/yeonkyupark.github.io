---
title: ggplot에서 부드러운 곡선 그리기
date: 2024-10-17
categories: interest
tags:
  - r
  - ggplot
image: /assets/images/logo_ggplot.png
toc: true
pin: false
math: true
mermaid: true
description: 실무에서 선그래프를 그리다 보면 꺽은 선보다 완만한 선이 필요한 경우가 있다. ggplot에서 완만한 곡선을 그리는 방법을 알아본다.
---
## ggplot에서 부드러운 곡선 그리기

`ggplot`에서 `geom_line`으로 선 그래프를 그리게 되면 아래와 같이 꺽은 선으로 나타난다. 현업을 하다 보면, 특히 발표 자료를 작성할 경우 내용상 문제는 없으나 미관상 완만한 곡선이 필요할 때가 있다.

```r
library(ggplot2)
library(ggalt)

df01 <- data.frame(
  month = c(1:12),
  sellout = sample(100:150, 12)
)

ggplot(df01, aes(x=month, y=sellout)) +
  geom_point() + geom_line()
```

![](/assets/images/Pasted%20image%2020241017002142.png)

### 방법1

`spline` 함수를 통해 점을 기준으로 완만한 선을 그릴 수 있도록 데이터를 늘려 준다. 그런 다음 `geom_line`을 통해 선그래프를 그리면 다음과 같다.

```r
# method 1
pts <- as.data.frame(spline(x=df01$sellout, n = 100))
ggplot(df01, aes(x=month, y=sellout)) +
  geom_line(data = pts, aes(x=x, y=y), linewidth = 2, color = "steelblue") +
  geom_point() + 
  geom_area(aes(x = x, y = y), data = pts, alpha = 0.2) +
  geom_text(aes(x = month + 0.3, y = sellout + 5, label = sellout)) +
  scale_x_continuous(breaks = 1:12)
```

![](/assets/images/Pasted%20image%2020241017002351.png)

### 방법2

`ggalt` 패키지 내 `geom_xspline()` 함수를 사용한다.

```r
# method 2
ggplot(df01, aes(x=month, y=sellout)) +
  geom_point() + geom_xspline() +
  geom_text(aes(x = month + 0.2, y = sellout + 2, label = sellout)) +
  scale_x_continuous(breaks = 1:12)
```

![](/assets/images/Pasted%20image%2020241017002504.png)

## Reference
1. [https://github.com/hrbrmstr/ggalt](https://github.com/hrbrmstr/ggalt)
2. [https://forum.posit.co/t/how-to-draw-a-smooth-line-connecting-all-points/182351/3](https://forum.posit.co/t/how-to-draw-a-smooth-line-connecting-all-points/182351/3)

_\_EOF\__
