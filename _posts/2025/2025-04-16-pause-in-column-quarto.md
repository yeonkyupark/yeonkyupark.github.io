---
title: Quarto Presentation 컬럼 안에서 pause 실행하기
date: 2025-04-16 
categories: [interest]
tags: [quarto, presentation]
image: /assets/images/logo_quarto.png
toc: true
pin: false
math: true
mermaid: true
description: quarto presentation 컬럼에서 pause 동작을 적용하는 방법을 알아 본다.
---

## Quarto Presentation 컬럼 안에서 pause 실행하기

Quarto Presentation에서는 Pause(다음 내용을 출력을 멈추는 기능)를 제공한다. 즉, 슬라이드 내 A 내용과 B 내용이 있고 이를 시간적으로 나누고 싶다면 pause(`. . .`) 키워드를 통해 구현할 수 있다.

```markdown
## Pause 적용하기

### A 내용

. . .

### B 내용
```

하지만 컬럼으로 슬라이드가 나누어진 경우 pause 기능을 동작하지 않는다.

### 컬럼 안에서는 fragment 사용하기

컬럼 안에서는 pause가 아닌 fragment를 사용해서 기능을 구현할 수 있다.

```markdown
## Pause 적용하기

:::{.columns}
:::{.column width="50%"}
### A 내용
:::

:::{.column width="50%"}

:::{.fragment}
### B 내용
:::

:::
:::
```

## 참고자료

1. https://quarto.org/docs/presentations/revealjs/advanced.html#fragments

