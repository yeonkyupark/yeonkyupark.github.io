---
title: 깃허브에서 블로그를 만들어 보자
date: 2023-10-14 09:14:00 +0900
categories:
  - hobby
tags:
  - github
  - jekyll
  - chirpy
---

지금껏 수많은 자료를 접하고 정리하고 사용했다. 하지만 지식 낱알은 모이지 못하고 이리 저리 흩어졌다. 여러 보조 수단을 사용했지만 그 때 잠시 뿐 지식은 모이지 못하고 지속성은 이내 곧 사그라졌다. 체계적으로 자료를 수집, 정리, 배포할 수 있는 방법을 고민했고 다음과 같은 방법으로 실천해 보기로 한다.

![Pasted image 20231015130218](https://github.com/yeonkyupark/yeonkyupark.github.io/assets/72383349/3a42556a-1842-4b76-be4f-0842dcd71d3c)

온/오프라인에서 수집할 수 있는 정보는 [옵시디언](https://obsidian.md/)을 통해 정리하고, 분류 체계에 따라 [깃허브](https://github.com/), [브런치,](https://brunch.co.kr/) [네이버블로그](https://section.blog.naver.com/)를 이용해서 배포하는 형태이다.

그 첫 번째 단계로 깃허브에 블로그를 설치해 본다.  깃허브와 깃허브 페이지는 이미 사용한 경험이 있다. 몇몇 저장소는 운영중이고 몇몇 저장소는 흔적도 없이 사라졌다. 블로그 형태인 `Pages` 서비스를 제공하고 있고 한 동안 잘 사용했었다. 지금은 디자인, 기능, 접근성 등 불편한 점이 있어 1년 이상 방치된 상태다.

자, 다시 가동을 시켜보자.

## 깃허브 계정 만들기

깃허브 계정은 인터넷 검색으로 해결하자. 수많은 중복 자료가 있을 듯 하다. 계정이 없다면 아래 계정 신청 사이트에서 만들도록 한다.

- 깃허브 계정등록: [Sign up](https://github.com/signup?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home)

## 적용할 테마 선정

깃허브 페이지에서도 몇몇 테마를 제공한다. 내용에 집중한다면 불편함 없이 사용이 가능하다고 생각된다. 하지만 심미적인 부분과 기능적인 부분에서 보이는 아쉬움은 어쩔 수 없는 듯 하다. 얼마 전 인터넷 검색을 통해 본 사이트는 깃허브에 블로그를 만들는 기회를 재공했다.

- 깔끔한 디자인
- 다양한 기능
- 문서 가독성
- 배포 편의성

검색을 통해 찾은 테마는 `Jekyll Theme` 중 인기 있는 ` Chirpy Theme`였다.

![image](https://github.com/yeonkyupark/yeonkyupark.github.io/assets/72383349/795d038c-0b84-4d5d-808b-94d13049b49c)

## 테마 환경 설정 및 적용

### 사전 준비

아래 준비물이 갖춰져 있어야 한다. 준비가 되었다면 [설치 가이드](https://chirpy.cotes.page/posts/getting-started/)에 따라 Config 설정 및 로컬에서 정상 동작을 확인한다.
- [Ruby](https://www.ruby-lang.org/ko/)
- [Jekyll](https://jekyllrb-ko.github.io/)
- [nodejs](https://nodejs.org/ko)

### 테마 다운로드

아래 방법 중 하나로 Chirpy 테마를 다운로드 받는다.

-  [**Using the Chirpy Starter**](https://chirpy.cotes.page/posts/getting-started/#option-1-using-the-chirpy-starter) - Easy to upgrade, isolates irrelevant project files so you can focus on writing.
- [**GitHub Fork**](https://chirpy.cotes.page/posts/getting-started/#option-2-github-fork) - Convenient for custom development, but difficult to upgrade. Unless you are familiar with Jekyll and are determined to tweak or contribute to this project, this approach is not recommended.
- [**Download ZIP**](https://github.com/cotes2020/jekyll-theme-chirpy/archive/refs/heads/master.zip)

### 의존성 점검

복사 또는 다운로드한 소스를 로컬 폴더에 저장한다. `bundle` 명령을 통해 의존성 점검을 진행합니다.

```
bundle
```

### 테마 환경 설정

\_config.yml 파일 내 일부 항목을 본인에 맞게 수정한다.

| 항목     | 값                              |
| -------- | ------------------------------- |
| lang     | ko                              |
| timezone | Asia/Seoul                      |
| title    | ㄴㄹㄱㅅㄴ                      |
| url      | "https://yeonkyupark.github.io" |
| avatar   | "/assets/img/avatar.jpg"        |

`avatar` 항목은 해당 경로에 해당 이미지 파일이 존재해야 한다.  이미지가 정상적으로 나오지 않으며 CDN 이미지 설정을 주석 처리 한다.

![Pasted image 20231014120029](https://github.com/yeonkyupark/yeonkyupark.github.io/assets/72383349/caf9e3ef-fbe8-4328-84da-c89745e93d1c)

```
# The CDN endpoint for images.
# Notice that once it is assigned, the CDN url
# will be added to all image (site avatar & posts' images) paths starting with '/'
#
# e.g. 'https://cdn.com'
img_cdn: # "https://chirpy-img.netlify.app"
```

### 로컬 서버에서 확인

아래 명령어로 로컬 서버 구동 및 수정 사항 반영을 확인한다.

```
bundle exec jekyll s
```

문제가 없다면 아래 주소로 접속이 가능하다.
-  _[http://127.0.0.1:4000](http://127.0.0.1:4000/)_

![Pasted image 20231014121205](https://github.com/yeonkyupark/yeonkyupark.github.io/assets/72383349/6df1385f-2336-40b4-ba1b-98df98882b63)

### GitHub commit

문제가 없다면 GitHub에 전체 폴더를 커밋한다. Repository는 \[gh_userid\].github.io로 설정한다.


## 최종 점검

### 빌드 및 배포 방식

아래 방법 중 하나를 선택한다.

#### GitHub Actions을 통한 빌드 및 배포

![](https://chirpy-img.netlify.app/posts/20180809/pages-source-dark.png)


#### 수동 빌드 및 배포

아래 명령어로 로컬에서 빌드한다. 

 ```
 $ JEKYLL_ENV=production bundle exec jekyll b
 ``` 

빌드된 소스는 GitHub 커밋 후 배포할 브랜치를 설정한다.

![Pasted image 20231014105153](https://github.com/yeonkyupark/yeonkyupark.github.io/assets/72383349/2cf232a7-9be3-40de-b75b-5f835c38601a)

### 배포된 사이트 확인

배포된 사이트는 `https://[gh_userid].github.io`로 접속하여 동작 여부를 확인할 수 있다.
