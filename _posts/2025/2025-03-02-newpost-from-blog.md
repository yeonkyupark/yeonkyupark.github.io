---
title: "블로그에서 Github에 새 글 등록하기"
date: "2025-03-02" 
categories: [hobby]
tags: [github]
image: /assets/images/logo_github.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

## 블로그에서 Github에 새 글 등록하는 방법

Github에서 운영중인 블로그에 글을 작성하려면 Github 사이트나 로컬에서 작성 후 commit을 했다. 블로그에서 바로 글을 작성할 수 있으면 편할 듯 하여 방법을 찾아봤다.

### 작성된 글 수정하기

일부 블로그에서 작성된 글을 수정할 수 있는 방법을 제공한다.

![글 수정 버튼](/assets/images/github_edit_this_page.png)

링크된 url을 살펴보면 다음과 같다.

```http
https://github.com/{owner}/{repo}/edit/{branch}/{filename}
```

위 Github 웹 UI 형태로 새 파일을 작성하면 될 듯 하다.

### 새 글 작성하기

`edit`를 `new`로 수정해서 url을 작성한다.

```http
https://github.com/{owner}/{repo}/new/{branch}
```

위와 같이 url을 호출하면 아래와 같이 새 파일을 작성할 수 있다.

![](/assets/images/github_new_file.png)

만약 파일 이름과 기본 내용을 포함해서 새 글을 작성하고 싶다면 filename, value 키워드를 사용한다.

```http
https://github.com/{owner}/{repo}/new/{branch}?filename=경로/파일명&vaule=기본값
```

아래는 본 블로그에 적용한 예시이다.

```http
https://github.com/yeonkyupark/yeonkyupark.github.io/new/main?filename=_posts/2025/2025-newpost.md&value=---%0Atitle:%20%0Adate:%20%20%0Acategories:%20[interest,%20hobby]%0Atags:%20[r,%20python]%0Aimage:%20/assets/images/logo_default.png%0Atoc:%20true%0Apin:%20false%0Amath:%20true%0Amermaid:%20true%0Adescription:%20%0A---%0A%0A
```

## 참고자료

1. [Github URL to create new file with specific name?](https://stackoverflow.com/questions/27778095/github-url-to-create-new-file-with-specific-name)
 
