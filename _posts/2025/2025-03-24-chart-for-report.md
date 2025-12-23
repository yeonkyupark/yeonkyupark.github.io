---
title: ggplot으로 보고서용 그래프 그리기 
date: 2025-03-24
categories: hobby
tags: [r, ggplot]
image: /assets/images/logo_ggplot.png
toc: true
pin: false
math: true
mermaid: true
description: 데이터 분석을 위한 시각화와 보고서용 시각화를 위한 그래프를 각각 작성해 본다.
keywords: ["r", "ggplot"]
---

## ggplot으로 보고서용 그래프 그리기

데이터 분석을 위해서는 미적인 부분보다 내용을 한눈에 파악할 수 있게 작성한다. 다만 보고서용으로 그래프를 작성한다만 minimal한 형태로 강조하고픈 부분을 집중하여 부각한다.

### 일반적인 형태 그래프

```r
# Normal
mtcars %>% 
  group_by(실린더 = as.factor(cyl), Automatic = as.factor(am)) %>% 
  reframe(모델수 = n()) %>% 
  ggplot(aes(x=실린더, y = 모델수, fill = Automatic)) +
  geom_col(position = "dodge") +
  theme_bw() + 
  theme(legend.position = "bottom")
```

![](/assets/images/2025-03-24-chart-for-report-1.png)

### 보고를 위한 그래프

```r
# Enhanced for report
mtcars %>% 
  group_by(실린더 = as.factor(cyl), Automatic = as.factor(am)) %>% 
  reframe(모델수 = n()) %>% 
  mutate(색상 = case_when(
    실린더 == "8" & Automatic == "0" ~ "salmon",
    실린더 == "8" & Automatic == "1" ~ "cornflowerblue",
    TRUE ~ "gray")) %>% 
  ggplot(aes(x=실린더, y = 모델수, fill = 색상, group = Automatic)) +
  geom_col(position = position_dodge2(width = 0.9, padding = 0.05)) +
  geom_text(aes(y=모델수, label = 모델수), 
            position = position_dodge2(width = 0.9, padding = 0.05), vjust = -0.5, size=3) +
  scale_fill_identity() +
  # theme_bw() + 
  theme(panel.grid.major = element_blank(), 
        panel.grid.minor = element_blank(), 
        panel.background = element_blank(), # ↑ theme_minimal()
        axis.ticks.x = element_line(color = "gray"),
        axis.ticks.y = element_line(color = "gray"), # ↑ axis.ticks = ...
        axis.line = element_line(colour = "gray"), 
        axis.title = element_text(color = "gray"),
        axis.text = element_text(color = "gray"),
        legend.direction = "horizontal",
        legend.position = c(0.15, 0.95))
```

![](/assets/images/2025-03-24-chart-for-report.png)

보고서 서식이나 도표는 보고 받는 사람 취향에 따라 선택하는 것이 가장 일을 효율적으로 하는 방법이다.

