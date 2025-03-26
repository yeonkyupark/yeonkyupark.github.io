---
title: Quarto Presenetation에서 나만의 제목 슬라이드를 만들어 보자
date: 2025-03-26 
categories: [hobby]
tags: [quarto, presentation]
image: /assets/images/logo_quarto.png
toc: true
pin: false
math: true
mermaid: true
description: quarto presentation에서 title slide를 사용자 요구에 맞도록 수정하는 방법을 알아 본다.
keywords: quarto, presentation, title slide, customization
---

## Quarto Presenetation에서 맞춤형 제목 슬라이드 만들기

Quarto Presentation에서 제공하는 제목 슬라이드 형식은 다음과 같다. 

```text
제목
부제목
저자
소속
날짜
```

![](/assets/images/2025-03-26-customize-title-slide-quarto.png){: .img-bordered}

위와 같이 기본 형식에서 필요에 따라 특정 정보를 추가로 표시해야 할 경우가 있다. 이때 어떻게 구현하는지 알아 본다.

### Frontmatter에 필요한 정보 추가하기

```yaml
# frontmatter in slide.qml
...
version: "1.0.0"
...
format:
  revealjs:
    template-partials:
      - title-slide.html
...
```

1. 제목 슬라이드에 "Ver 1.0.0"을 출력하기 위해 `qmd` 파일에 `version` frontmatter를 추가한다.
2. 원하는 layout을 구성하기 위한 template을 추가한다.

### custom template 작성

아래 내용을 기반으로 원하는 layout을 구성한다.

- https://github.com/quarto-dev/quarto-cli/blob/main/src/resources/formats/revealjs/pandoc/title-slide.html

```html
<section id="$idprefix$title-slide"$for(title-slide-attributes/pairs)$ $it.key$="$it.value$"$endfor$>
  <h1 class="title">$title$</h1>
$if(subtitle)$
  <p class="subtitle">$subtitle$</p>
$endif$

<!-- horizontal line -->
<hr border=1 solid color="gray">

<!-- version -->
$if(version)$
  <p class="subtitle">Ver $version$</p>
$endif$

$for(author)$
  <p class="author">$author$</p>
$endfor$
$for(institute)$
  <p class="institute">$institute$</p>
$endfor$
$if(date)$
  <p class="date">$date$</p>
$endif$
</section>
```

위 예제에서는 subtitle 밑에 수평선을 긋고 그 밑에 버전을 출력하는 형식이다.

작성된 파일은 `title-slide.html`로 root 폴더에 저장한다.

### 결과물 확인하기

최종 rendering된 결과물을 확인한다.

![](/assets/images/2025-03-26-customize-title-slide-quarto-1.png){: .img-bordered}


## 참고자료
1. [Custom Template](https://quarto.org/docs/presentations/revealjs/advanced.html#custom-template)