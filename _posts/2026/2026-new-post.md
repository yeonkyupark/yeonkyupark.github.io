---
title: Chirpy Theme 포스트에 수정 버튼 달기
date: 2026-01-04
categories: [hobby]
tags: [chirpy]
image: /assets/images/logo_chirpy.png
toc: true
pin: false
math: true
mermaid: true
description: chirpy 테마에 수정하기 버튼을 구현한다.
---

Quarto Book은 UI에서 “Edit this page” 기능이 있다. 현 페이지를 외부에서 쉽게 접근하여 내용을 추가하거나 오타를 수정하는 등 사용 편의성을 제공한다. Chirpy 테마에서도 같은 기능을 제공하는 수정 버튼을 추가해 본다.

## 수정하기 버튼 구조

수정하기 버튼은 다음가 같은 주소로 접근한다.

```
https://github.com/사용자이름/저장소이름/edit/브랜치이름/파일경로
```

Jekyll에서 제공하는 변수를 적용하면 다음과 같다.

```
{{ site.github.repository_url }}/edit/{{ site.github.build_revision | default: "main" }}/{{ page.path }}
```

## 수정하기 버튼 적용

게시글을 출력하는 `_layout/post.html`을 편집하여 구현한다. 만약 코드 내 해당 파일이 없다면 Chirpy 원본 저장소에서 복사하여 사용한다.

- https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/_layouts/post.html 

해당 파일 내 원하는 위치에 아래 코드를 추가한다.

```
<a href="https://github.com/{{ site.github.username }}/{{ site.github.repository }}/edit/main/{{ page.path }}" target="_blank" rel="noopener">
  <i class="fas fa-pen fa-sm"></i> Edit this page
</a>
```

구현 내용이 정상동작하도록 `_config.yml` 파일에 아래 정보를 추가한다.

```
github:
  username: githubid              # github 계정
  repository: githubid.github.io  # 저장소 이름
```

## 결과 확인하기

`lastmod date` 다음에 버튼을 추가한다.

```html
      <!-- lastmod date -->
      {% if page.last_modified_at and page.last_modified_at != page.date %}
        <span>
          {{ site.data.locales[lang].post.updated }}
          {% include datetime.html date=page.last_modified_at tooltip=true lang=lang %}
        </span>
      {% endif %}

<!-- Edit this page 추가 [[ -->
      <span>        
        <a href="https://github.com/{{ site.github.username }}/{{ site.github.repository }}/edit/main/{{ page.path }}" target="_blank" rel="noopener">
        <i class="fas fa-pen fa-sm"></i> Edit this page</a>
      </span> 
<!-- Edit this page 추가 ]] -->

```

![](/assets/images/Pasted%20image%2020260104070701.png)


_\_EOF\__
