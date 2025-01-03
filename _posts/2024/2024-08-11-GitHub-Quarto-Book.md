---
title: GitHub와 Quarto Book을 연동하자
date: 2024-08-11
categories: hobby
tags:
  - quarto
  - github
---
## GitHub와 Quarto Book을 연동하자
GitHub와 Quarto로 작성한 Book을 연동하고 GitHub Action으로 자동 빌드 및 배포하는 과정을 정리했다.

> 전제 조건
> - GihHub에 계정이 있고 기본적인 사용 방법을 숙지하고 있다.
> - R-Studio를 사용할 수 있다.
> - Quarto를 이용하여 문서(Website, Blog, Book 등)를 작성할 수 있다.

## GitHub 작업
GitHub에 Repository를 생성하는 방법은 다양할 수 있으나 개인적으로 진행하는 방법은 아래와 같다. GitHub site → Repositories → `New`를 통해 생성한다.  

![](/assets/images/Pasted%20image%2020240811114327.png)

개인 취향에 따라 `.gitignore` 파일을 추가한다.

![](/assets/images/Pasted%20image%2020240811114338.png)


Repository를 생성하고 나면 local 폴더에 복사(clone) 한다. 아래는 GitHub Desktop을 이용한 경우이다.

![](/assets/images/Pasted%20image%2020240811114349.png)
## RStudio 작업
RStudio에서 새 프로젝트를 생성한다.

![](/assets/images/Pasted%20image%2020240811114406.png)

![](/assets/images/Pasted%20image%2020240811114411.png)

프로젝트 생성 시 반드시 빈 폴더를 생성한다. 파일이 있는 기존 폴더를 사용할 경우 아래와 같은 경고 문구와 함께 프로젝트는 생성되지 않는다.

![](/assets/images/Pasted%20image%2020240811114427.png)

임시 폴더명을 설정하고 프로젝트를 생성한다.

![](/assets/images/Pasted%20image%2020240811114435.png)

RStudio를 종료하고 생성된 프로젝트의 모든 파일을 GitHub와 연결된 폴더로 이동하다.

![](/assets/images/Pasted%20image%2020240811114443.png)

![](/assets/images/Pasted%20image%2020240811114445.png)

필요하다면 `.Rproj` 파일을 적당한 이름으로 변경한다. `.Rproj` 파일을 실행하여 RStudio를 연다.
## Quarto Book 작성

`GitHub Action`을 이용하기 위해 `_quarto.yml` 파일을 수정한다. 자동 빌드된 후 산출물이 저장될 디렉토리를 아래와 같이 설정한다.

![](/assets/images/Pasted%20image%2020240811114453.png)

 `_quarto.yml` 파일 내 `title`, `author` 정도만 간단히 수정하고 지금까지 진행된 파일을 GitHub에 올린다.
 
## GitHub와 Quarto 연동

GitHub Desktop을 사용한다면 다음과 같이 추가된 파일이 `commit` 되어 있을 것이다. `push` 한 후 GitHub에 정상적으로 업로드 되었는지 확인하다.

![](/assets/images/Pasted%20image%2020240811114504.png)

![](/assets/images/Pasted%20image%2020240811114506.png)

이제 main 브랜치에 내용이 수정되면 자동으로 빌드 후 산출물을 `/docs` 폴더에 저장된다. 이 저장된 산출물을 `gh-pages` 브랜치로 옮겨 인터넷을 통해 볼 수 있도록 배포하는 설정을 한다.

### gh-pages 브랜치 생성하기
아래 명령을 통해 `gh-pages` 브랜치를 생성한다.

![](/assets/images/Pasted%20image%2020240811114521.png)

![](/assets/images/Pasted%20image%2020240811114523.png)

실행이 완료된 후 GitHub에서 `gh-pages` 브랜치가 정상적으로 생성되었는지 확인한다.

![](/assets/images/Pasted%20image%2020240811114531.png)

GitHub에서 Jekyll을 사용하지 않도록 아래와 같이 `.nojekyll` 파일을 추가한다.

```
copy NUL .nojekyll
```

GitHub Action을 `.github/workflows/publish.yml` 경로에 아래와 같이 작성한다.

```
on:
  workflow_dispatch:
  push:
    branches: main

name: Quarto Publish

jobs:
  build-deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Check out repository
        uses: actions/checkout@v4
        
      - uses: r-lib/actions/setup-r@v2
      - uses: r-lib/actions/setup-r-dependencies@v2
        with:
          packages:
            any::rmarkdown
            any::knitr
      - uses: r-lib/actions/setup-tinytex@v1

      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2
        
      - name: Render and Publish
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Action이 정상적으로 작성되었다면 `Actions` 메뉴를 통해 동작 여부를 확인할 수 있다.

![](/assets/images/Pasted%20image%2020240811114551.png)

Action이 정상 수행되면 `/docs` 폴더가 생성되고 산출물이 `gh-pages` 브랜치로 복사되어 배포가 된다. `Settings` 메뉴를 통해 배포된 결과물을 확인할 수 있다. Action 수행 중 상황에 따라 다양한 오류가 발생할 수 있는데[^1][^2][^3] 인터넷 검색을 통해 하나씩 해결해야 한다.

`publish.yml`이 정상적으로 동작한다면 배포된 사이트에 접속하여 내용을 확인할 수 있다.

![](/assets/images/Pasted%20image%2020240811114603.png)

![](/assets/images/Pasted%20image%2020240811114605.png)

마지막으로 파일을 수정하여 자동 빌드 및 배포가 되는지 확인한다.

![](/assets/images/Pasted%20image%2020240811114617.png)

![](/assets/images/Pasted%20image%2020240811114620.png)



[^1]: https://stackoverflow.com/questions/74885595/quarto-book-publish-produces-latex-error-file-scrreprt-cls-not-found
[^2]: https://github.com/quarto-dev/quarto-cli/issues/5870
[^3]: https://github.com/r-lib/actions/issues/213


_\_EOF\__
