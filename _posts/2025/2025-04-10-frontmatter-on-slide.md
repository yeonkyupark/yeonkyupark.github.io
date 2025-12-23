---
title: Quarto Presentation Frontmatter를 슬라이드에 출력하기
date: 2025-04-10 
categories: [hobby]
tags: [r, quarto]
image: /assets/images/logo_quarto.png
toc: true
pin: false
math: true
mermaid: true
description: Quarto Presentation Frontmatter를 슬라이드에 출력하는 방법을 알아본다.
version: "1.0.0"
---

## Quarto Presentation Frontmatter를 슬라이드에 출력하기

### Frontmatter 설정

```yaml
---
title: "My Presentation"
version: "1.0.0"
format: revealjs
---
```

### 슬라이드 본문에 출력

출력할 위치에 아래와 같이 입력한다.

```markdown
Version: {% raw %}{{< meta version >}}{% endraw %}
```

작성자, 버전 등 슬라이드 상단이나 하단에 정보 표기할 때 유용하게 활용 가능하다.

## 참고자료

1. [Quarto Guide > Advanced > Variables](https://quarto.org/docs/authoring/variables.html)
