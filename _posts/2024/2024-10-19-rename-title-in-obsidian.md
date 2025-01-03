---
title: 새 문서 작성 시 파일 이름 변경하기
date: 2024-10-19
categories: hobby
tags:
  - obsidian
  - plugin
image: /assets/images/logo_obsidian.png
toc: true
pin: false
math: true
mermaid: true
description: 옵시디언(Obsidian)에서 새 파일 작성 시 파일 제목을 형식에 맞춰 변경하는 방법을 알아본다.(feat. Templater).
---

## 새 문서 작성

**옵시디언**(Obsidian)에서 새 파일을 생성하게 되면 기본 파일명은 `Untitled`이다.  상황에 따라 파일명을 특정 양식(format)으로 맞춰야 할 때가 있다. 블로그에 등록할 파일 제목명이라든지, 옵시디언 내 특정 폴더에 문서를 저장하기 위해서 등이 그런 경우이다. `Templater` [^1]플러그인(plugin)을 사용하면 이런 일련의 작업을 쉽게 진행할 수 있다.

[^1]: [https://silentvoid13.github.io/Templater/](https://silentvoid13.github.io/Templater/)

### Templater 플러그인 설치

![](/assets/images/2024-10-19-rename-title-in-obsidian-templater.png)

### Template 파일 생성

새 문서를 작성할 때 기본 양식으로 사용한 파일을 생성한다.

```md
---
title: 
date: <% tp.date.now() %>
---

## 제목


<% await tp.file.move("_posts/2024/" + tp.file.title) %>
<% tp.file.rename(tp.date.now()+"-") %>
```

위 코드는 새 파일을 생성하면 `_posts/2024/` 폴더로 이동시키는 코드와 파일명 prefix를 `202-10-19-`로 설정하는 코드이다.

### 새 파일 생성하기

![](/assets/images/2024-10-19-rename-title-in-obsidian-new-note.png)
![](/assets/images/2024-10-19-rename-title-in-obsidian-new-note2.png)

Templater 명령어를 사용하여 작성한 템플릿을 적용한 파일을 생성한다. 그러면 아래 파일이 `_posts\2024` 폴더에 생성된다.

![](/assets/images/2024-10-19-rename-title-in-obsidian-new-note3.png)

