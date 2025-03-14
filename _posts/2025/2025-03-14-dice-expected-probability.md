---
title: 주사위를 던졌을 때 기대값 계산
date: 2025-03-14 
categories: [interest]
tags: [r, wrangling]
image: /assets/images/logo_wrangling.png
toc: true
pin: false
math: true
mermaid: true
description: 주사위, 확률, 기대값
---

## 주사위를 던졌을 때 기대값 계산

주사위는 1부터 6까지 숫자를 갖고 던지게되면 동일한 확률로 6개중 숫자 하나가 나오게 된다. 주사위를 여러 번 던지게 되면 기대값이 어떻게 되는지 계산해 본다.

```r
dice <- c(1,2,3,4,5,6)

trial <- c()
for(i in 1:100){
  trial <- c(trial, mean(sample(dice, 2, replace=T)))
}

m <- mean(trial)
s <- sd(trial)

h <- hist(trial, main = NULL, xlab = NULL, ylab = NULL)
xfit <- seq(min(trial), max(trial), length = length(trial))
yfit <- dnorm(xfit, mean = m, sd = s)
yfit <- yfit*diff(h$mids[1:2])*length(trial)
lines(xfit, yfit, col="blue", lwd=2)
abline(v = m, col = "red", lwd=2, lty=2)
```

위 코드는 주사위 2개 던져 평균을 시행을 100번 한 결과 아래와 같은 결과를 얻는다(평균: 3.63).

![](/assets/images/2025-03-14-dice-expected-probability.png)
주사위 개수와 시행 횟수가 늘어 날수록 정규분포에  가까워진다. 아래 결과는 주사위 10개, 1000회 시험 결과이다(평균: 3.49, 분산: 0.53^2).
![](assets/images/2025-03-14-dice-expected-probability-1.png)
