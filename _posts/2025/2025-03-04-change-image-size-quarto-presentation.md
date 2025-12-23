---
title: Quarto Presentation에서 이미지 크기 조절하기 
date: 2025-03-04 
categories: [interest]
tags: [quarto]
image: /assets/images/logo_quarto.png
toc: true
pin: false
math: true
mermaid: true
description: Quarto Presentation 이미지 크기는 확장이 기본 옵션이다. Presentation 크기보다 작은 경우 이미지가 확장되면서 화질이 저하된다. 이를 방지하기 위해 .nostretch 옵션을 사용한다.
---

## Quarto Presentation에서 이미지 크기 조절하기

![기본 설정](/assets/images/image_nostreched_00.png)

Quarto Presentation에서는 기본값으로 이미지 크기가 확장(streched)된다. Presentation layout size보다 작으면 이미지를 확대해서 해상도가 낮아지는 단점이 있다. 원본 크기를 유지하기 위해서는 아래와 가이드를 참고한다.

- https://quarto.org/docs/presentations/revealjs/advanced.html#stretch

### YAML에 옵션 추가

YAML header에 아래와 같이 옵션을 추가하다.

```yaml
format:
  revealjs:
    auto-stretch: false
```
![옵션 1](/assets/images/image_nostreched_01.png)

### 슬라이더 타이틀에 옵션 추가

```markdown
## Slide Title {.nostretch}
```

![옵션 2](/assets/images/image_nostreched_02.png)


### 이미지에 직접 옵션 추가

```markdown
![](image.png){.nostretch fig-align="center" width="800px"}
```

![옵션 3](/assets/images/image_nostreched_03.png)

## 참고자료

1. [How to resize image in Quarto revealjs presentation](https://github.com/quarto-dev/quarto-cli/discussions/5701)
2. [Guide > Presentations > Revealjs > Advanced Reveal > Layout Helpers > Stretch](https://quarto.org/docs/presentations/revealjs/advanced.html#stretch)

