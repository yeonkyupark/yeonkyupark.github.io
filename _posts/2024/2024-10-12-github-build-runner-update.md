---
title: github build runner update
date: 2024-10-12
categories: hobby
tags:
  - github
  - jekyll
image: /assets/images/Pasted%20image%2020241012191128.png
description: GitHub Actions 빌드 에러 수정
---

## GitHub build runner update
10월에 작성한 글이 GitHub Actions을 돌면서 build runner 관련 error를 발생시켰다. GitHub Actions을 잘 모르기에 수정하기가 만만치 않았다. 인터넷 검색도 해 봤지만 적절한 답을 찾지 못했다.

이런 저런 시행착오 끝에 동작하도록 조치는 했다. 하지만 사이트를 정상적으로 운영하려면 GitHub Actions 공부를 좀 해야겠다.

```
jobs:
  # Build job
  build:
    # runs-on: ubuntu-latest
    if: true
    strategy:
      fail-fast: false
      matrix:
        os: [ ubuntu-20.04 ]
        ruby: [ruby-3.4.0-preview2]
    runs-on: $ {{ matrix.os }}
```

`runs-on`에 명시적으로 `ubuntu-20.04`를 적어 두던지 아래 참고 자료 내용을 적용해도 된다.

- [*https://github.com/ruby/ruby-builder/blob/master/.github/workflows/build.yml*](https://github.com/ruby/ruby-builder/blob/master/.github/workflows/build.yml)


_\_EOF\__
