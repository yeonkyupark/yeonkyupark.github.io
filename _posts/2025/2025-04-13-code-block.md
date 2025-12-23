---
title: 렌더링에 따른 코드블록 출력 오류 해결하기
date: 2025-04-13 
categories: [hobby]
tags: [blog]
image: /assets/images/logo_default.png
toc: true
pin: false
math: true
mermaid: true
description: 렌더링 플랫폼에 따라 코드블록 내 코드를 정상적으로 출력하지 못하는 경우가 있다. 이런 경우 사용할 수 있는 해결책을 알아 본다.
---

## 렌더링에 따른 코드블록 출력 오류 해결하기

블로그 작성시 렌더링 플랫폼에 따라 코드블록이 정상적으로 출력되지 않는 경우가 있다. 예를 들면 Quarto에서 변수로 사용하는 {% raw %}`{{< meta 변수 >}}`{% endraw %} 구문이나 Hugo 스타일에서 사용하는 shortcodes {% raw %}`{{<  >}}`{% endraw %} 등을 사용할 경 jekyll에서 렌더링시 코드블록이 정상적으로 출력되지 않는다. 즉, 해당 코드가 사라지는 문제가 발생한다.

이런 문제를 해결할 수 있는 몇가지 방법을 알아 본다.

### &#123;% raw %&#125; 블록 사용

{% raw %}
```markdown
Version: {{< meta version >}}
```
{% endraw %}

### 중괄호를 코드로 표기


또는 아래와 같이 HTML entity를 이용한 표현도 가능하다(`&#123; → {`, `&#125; → }`).

> Version: &#123;&#123;< meta version >&#125;&#125;


### `<pre><code>` 태그 사용

```html
<pre><code>
  Version: {{< meta version >}}
</code></pre>
```


이건 렌더링에 따라 될, 또는 안될 수도 있다.

상황에 맞춰 선호하는 방법을 적용한다.

## 참고자료



