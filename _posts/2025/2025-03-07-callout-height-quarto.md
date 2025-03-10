---
title: Quarto Presentation에서 Callout 높이 맞추기
date: 2025-03-07 
categories: [hobby]
tags: [quarto]
image: /assets/images/logo_quarto.png
toc: true
pin: false
math: true
mermaid: true
description: quarto presentation callout 높이 맞추기 
---

## Quarto Presentation에서 Callout 높이 맞추기

Quarto Presentation에서 내용을 강조하기 위해 Callout을 사용할 수 있다.

```markdown
::: {.callout-note}

## Pay Attention

Using callouts is an effective way to highlight content that your reader give special consideration or attention.

:::
```

![](/assets/images/20250307_callout_height.png)

위 예제처럼 Callout 높이는 내용에 맞춰 설정된다. 따라서 컬럼으로 배치할 경우 내용에 따라 높이가 다르게 되어 가시성이 저하될 수 있다.

```markdown
:::: {.columns}
::: {.column width="50%"}
::: {.callout-note}

## Pay Attention1

Using callouts is an effective way to highlight content that your reader give special consideration or attention.

:::
:::
::: {.column width="50%"}
::: {.callout-note}

## Pay Attention2

Using callouts is an effective way to highlight content that your reader give special consideration or attention.
Using callouts is an effective way to highlight content that your reader give special consideration or attention.
Using callouts is an effective way to highlight content that your reader give special consideration or attention.

:::
:::
::::
```
![](/assets/images/20250307_callout_height_01.png)

## div style을 통해 같은 높이 설정
다양한 방법이 있겠지만 단순, 직관적으로 div 태그 내 style 옵션으로 높이를 설정한다.

```markdown
:::: {.columns}
::: {.column width="50%"}
::: {.callout-note}

## Pay Attention1

<div style="height:350px;">
Using callouts is an effective way to highlight content that your reader give special consideration or attention.
</div>

:::
:::
::: {.column width="50%"}
::: {.callout-note}

## Pay Attention2

<div style="height:350px;">
Using callouts is an effective way to highlight content that your reader give special consideration or attention.
Using callouts is an effective way to highlight content that your reader give special consideration or attention.
Using callouts is an effective way to highlight content that your reader give special consideration or attention.
</div>

:::
:::
::::

```

![](/assets/images/20250307_callout_height_02.png)

## 참고자료
1. [Guide > Authoring > Callout Blocks](https://quarto.org/docs/authoring/callouts.html)
1. [How do I create cards/callouts of the same height and positioned next to each other?](https://github.com/quarto-dev/quarto-cli/discussions/9213)
