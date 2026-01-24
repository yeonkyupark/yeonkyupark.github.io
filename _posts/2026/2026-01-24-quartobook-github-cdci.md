---
title: Quarto Book을 GitHub를 통해 자동 빌드 및 배포하기
date: 2026-01-24
categories: [hobby]
tags: [rstudio, quarto, github]
image: /assets/images/logo_quarto.png
toc: true
pin: false
math: true
mermaid: true
description: Quarto Book을 GitHub를 통해 자동 빌드 및 배포하는 절차를 알아 본다.
---

Web book을 제작하는 도구 중 하나로 Quarto가 있다. RStudio나 타 편집기를 이용하면 효율적으로 문서 작성이 가능하다. 특히 R이나 파이썬 등을 이용하는 경우 그 효과는 배가 된다.
리눅스 환경에서 Quarto 문서를 제작하고 GitHub에서 소스를 관리하는 구조로 구현한다. 저장소에 변경 사항이 발생하면 GitHub Actions를 통해 자동 빌드 및 배포까지 진행한다.

**전제**
- 리눅스 환경
- GitHub 계정 보유

먼저 전체 흐름을 살펴보면 다음과 같다.

1. GitHub에 저장소 생성
2. 로컬에서 Quarto Book 프로젝트 생성
3. GitHub 저장소와 연결
4. Quarto Book 기본 설정
5. GitHub Action 설정
6. GitHub Pages 설정
7. 로컬 수정 또는 GitHub 수정 후 자동 배포 확인

## GitHub 저장소 생성

GitHub 로그인 후 우측 상단에서 `New repository` 메뉴를 통해 새로운 저장소를 생성한다.


## Quarto Book 프로젝트 생성

로컬에서 `RStudio` > `Quarto Book` 프로젝트를 생성한다. 또는 다음과 같이 터미널에서 생성할 수도 있다.

```
mkdir ~/Projects
cd ~/Projects

quarto create-project quarto-book --type book
Creating project at /home/yk/Projects/quarto-book:
  - Created _quarto.yml
  - Created index.qmd
  - Created intro.qmd
  - Created summary.qmd
  - Created references.qmd
  - Created cover.png
  - Created references.bib
```

## GitHub 저장소 연결

프로젝트가 생성된 로컬 폴더로 이동하여 git을 초기화 한다.

```
git init
```

생성한 GitHub 저장소와 연결한다.

```
git remote add origin https://github.com/USERNAME/quarto-book.git
```

생성된 프로젝트 내 파일을 GitHub에 업로드(commit & push)한다.

```
git add .
git commit -m "init quarto book"
git branch -M main
git push -u origin main
```

만약 `.gitignore`나 `README` 파일 등 저장소에 내용이 있다면 아래와 같이 pull을 통해 먼저 상태를 정리한다.

```
git pull origin main --no-rebase --allow-unrelated-histories
```

GitHub에서 정상 업로드 되었는지 확인한다. 

## Quarto Book 설정

```
project:
  type: book

book:
  title: "My Quarto Book"
  author: "Your Name"
  site-url: https://USERNAME.github.io/quarto-book/
  chapters:
    - index.qmd
    - intro.qmd
    - summary.qmd
    - references.qmd

format:
  html:
    theme: cosmo

execute:
  freeze: auto
```

`_quarto.yml`을 상황에 맞춰 설정한다. 특히 `site-url`은 자동 배포 후 웹을 통해 확인해야 하는 경로가 된다.

## GitHub Actions 설정

변경 사항이 있으면 GitHub Actions를 통해 자동 빌드되도록 설정한다.

Actions가 동작하도록 아래와 같이 경로를 생성한다.

```
mkdir -p .github/workflows
```

실제 동작할 workflow 파일을 생성한다.

```
nano .github/workflows/quarto-publish.yml
```

```
name: Render and Publish Quarto Book

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  build-deploy:
    runs-on: ubuntu-latest

    permissions:
      contents: write

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Quarto
        uses: quarto-dev/quarto-actions/setup@v2

      - name: Render Quarto Book
        run: |
          quarto render

      - name: Publish to GitHub Pages
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages

```

Actions가 `gh-pages`에 정상 동작할 수 있도록 브랜치를 생성해 준다. 프로젝트 폴더에서 아래 명령을 실행한다.

```
quarto publish gh-pages
```

현재까지 진행된 내용을 GitHub Pages에서 출력하도록 `gh-pages`에 작업을 한다. 이후 workflow에 따라 자동 빌드 및 배포가 진행된다. 

이제 워크플로를 업로드 한다.

```
git add .github/workflows/quarto-publish.yml
git commit -m "add github actions for quarto publish"
git push
```

## GitHub Pages 설정

Quarto Book으로 작성된 내용이 Pages로 출력되도록 설정한다. 저장소 > Settings > Pages로 이동하여 다음 항목을 수정한다.

- Source
	- Deploy from a branch
- Branch
	- gh-pages
	- / (root)

이상 없이 여기까지 진행되었다면 `site_url`인 `https://USERNAME.github.io/quarto-book/`에서 배포 내용을 확인할 수 있다.

## 자동 빌드 및 배포 확인

자동 빌드 및 배포를 확인하기 위해 index.qmd 파일을 수정 후 site_url에서 확인하다.


_\_EOF\__
