---
title: Jekyll Chirpy 테마에 배너 달기
date: 2024-10-20
categories: hobby
tags:
  - jekyll
  - chirpy
image: /assets/images/logo_chirpy.png
toc: true
pin: false
math: true
mermaid: true
description:
---
## Jekyll Chirpy 테마에 배너 달기

Jekyll Chirpy 테마에 아래와 같이 배너를 추가하는 방법이다[^1].  

![](/assets/images/2024-10-20-banner-in-chirpy.png)

## 배너에 표시할 내용 만들기

아래와 같이 배너에 표시할 내용을 작성하여 `/_includes` 폴더 밑에 저장한다(예, `my_notice.html`).

```html
<div class="box-info">
<div class="title"> 새소식 </div>
- Chirpy Theme 7.1.1 업데이트
</div>
```

## 배너 배치하기

배너를 출력할 적당한 위치를 선정한다. 본 예에서는 개별 게시물 상단에 출력한다. 따라서 개별 게시물과 관련된 `/layouts/post.hmtl` 파일을 아래와 같이 수정한다.
{% raw %}
```html
---
layout: default
refactor: true
panel_includes:
  - toc
tail_includes:
  - related-posts
  - post-nav
  - comments
---

{% include lang.html %}

{% include toc-status.html %}

{% include my_notice.html %} <!-- 여기에 작성한 배너 파일을 추가한다 -->


<article class="px-1" data-toc="{{ enable_toc }}">
  <header>
    <h1 data-toc-skip>{{ page.title }}</h1>
    {% if page.description %}
      <p class="post-desc fw-light mb-4">{{ page.description }}</p>
    {% endif %}

```
{% endraw %}

`toc-status.html`과 `<article>` 영역 사이에 작성한 배너를 삽입한다. 이때 작성한 배너 파일명과 동일한지 확인한다. 특별한 문제가 없다면 첫 이미지와 같이 게시물 상단에 공지사항을 표시할 수 있다.

> chirpy-starter[^2]로 테마를 적용한 경우 `/_includes`, `/_layouts` 폴더가 없다. [jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)에서 복사하여 본인 소스에 붙여 넣는다.    
{: .prompt-warning}


> `prompt`와 유사한 `box`[^3]를 사용하기 위해서는 `assets/css/jekyll-theme-chirpy.scss` 파일에 아래 [관련 코드](https://github.com/cotes2020/jekyll-theme-chirpy/discussions/1707)를 추가한다.  
{: .prompt-info}

## 참고자료

[^1]: [EP25. 블로그에 상단 배너 추가하기](https://www.youtube.com/watch?v=fo3tpjxZbZQ&list=PLIMb_GuNnFwfMm3alTSOmDK4AnpdG7USY&index=12)

[^2]: [https://github.com/cotes2020/chirpy-starter](https://github.com/cotes2020/chirpy-starter)

[^3]: [https://github.com/cotes2020/jekyll-theme-chirpy/discussions/1707](https://github.com/cotes2020/jekyll-theme-chirpy/discussions/1707)