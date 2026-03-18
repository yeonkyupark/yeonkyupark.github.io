---
title: VSCode와 Quarto를 이용한 Web 제작
date: 2026-03-18
categories: [hobby]
tags: [quarto]
image: /assets/images/logo_quarto.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

다음은 **VSCode + Quarto + uv + GitHub Actions 기반 Python 기술 문서 자동 배포 구축 전체 가이드 **이다.

---

# 개요

Visual Studio Code, Quarto, GitHub, uv를 활용하여

* Python 기술 문서 작성
* 실행 가능한 코드 포함 (Jupyter 기반)
* GitHub Actions로 자동 배포 (CI/CD)

환경을 구축한다.

---

# 1. 개발 환경 구축

## 1.1 필수 설치

* Python
* VSCode
* Quarto

확장 프로그램:

* Python
* Jupyter
* Quarto

---

## 1.2 uv 설치

```bash
pip install uv
```

---

## 1.3 Quarto 설치 확인

```bash
quarto check
```

---

# 2. Quarto 프로젝트 생성

```bash
quarto create project book eda-for-python
cd eda-for-python
code .
```

---

# 3. uv 환경 구성

## 3.1 초기화

```bash
uv init
```

---

## 3.2 패키지 설치

```bash
uv add numpy pandas matplotlib seaborn jupyter ipykernel
```

---

## 3.3 실행

```bash
uv run quarto preview
```

---

# 4. 문서 작성

*_quarto.yml*:

```yaml
project:
  type: book

book:
  title: "EDA for Python"
  author: "YK"
  date: "2026. 3. 18."
  chapters:
    - index.qmd

format:
  html:
    theme:
      - cosmo
      - brand
```

---

*index.qmd*: 

````markdown
# 들어가기 {.unnumbered}

```{python}
import seaborn as sns

df = sns.load_dataset('penguins')
df.head()
```
````

---

# 5. gitignore 설정 (중요)

*.gitignore*: 

```gitignore
.venv/
.quarto/
_site/
__pycache__/
.ipynb_checkpoints/
_book/
_freeze/
```

포함해야 할 파일:

```text
pyproject.toml
uv.lock
```

---

# 6. GitHub 연결

## 6.1 초기화

```bash
git init
git add .
git commit -m "init project"
```

---

## 6.2 원격 연결

```bash
git remote add origin https://github.com/사용자명/eda-for-python.git
git branch -M main
git push -u origin main
```

---

# 7. GitHub Pages 설정

* Settings → Pages
* Source → GitHub Actions

---

# 8. 최초 배포

```bash
uv run quarto publish gh-pages
```

---

# 9. GitHub Actions 구성

*.github/workflows/publish.yml*: 

```yaml
name: Publish Quarto Book (uv)

on:
  push:
    branches: [main]

permissions:
  contents: write

jobs:
  build-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Install uv
        run: pip install uv

      - name: Install dependencies
        run: |
          uv sync
          uv run python -m ipykernel install --user --name python3

      - name: Setup Quarto
        uses: quarto-dev/quarto-actions/setup@v2

      - name: Render
        run: uv run quarto render

      - name: Publish
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
```

---

# 10. CI/CD 동작 확인

```bash
git add .
git commit -m "update"
git push
```

확인:

* Actions 실행 여부
* gh-pages 브랜치 생성
* 웹 페이지 반영

접속:

```text
https://사용자명.github.io/eda-for-python/
```

---

# 11. 핵심 실행 구조

```text
uv 환경
  ↓
jupyter + ipykernel
  ↓
quarto render
  ↓
gh-pages 배포
```

---

# 12. 주요 에러 및 해결

## 12.1 nbformat 없음 에러

```text
ModuleNotFoundError: No module named 'nbformat'
```

원인:

* 시스템 Python 사용

해결:

```bash
uv add jupyter ipykernel
```

workflow에 추가:

```yaml
uv run python -m ipykernel install --user --name python3
```

---

## 12.2 uv.lock 파싱 에러

```text
extra `=`, expected nothing
```

원인:

* pip 스타일 lock 파일 사용

해결:

```bash
rm uv.lock
uv sync
```

금지:

```bash
uv pip compile
```

---

## 12.3 권한 에러 (403)

```text
Permission denied to github-actions[bot]
```

해결:

```yaml
permissions:
  contents: write
```

추가 확인:

* Settings → Actions → Read and write permissions

---

## 12.4 gh-pages 브랜치 없음

```text
does not have a branch named gh-pages
```

해결:

```bash
uv run quarto publish gh-pages
```

---

## 12.5 404 Not Found

원인:

* Pages 설정 안됨
* URL 오류
* 배포 지연

확인:

```text
Settings → Pages → GitHub Actions
https://username.github.io/repo/
```

---

## 12.6 PowerShell activate 오류

```text
PSSecurityException
```

해결:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

# 13. uv 사용 규칙

사용:

```bash
uv add 패키지
uv sync
uv run 명령어
```

금지:

```bash
uv pip compile
uv pip sync uv.lock
```

---

# 14. 프로젝트 구조

```text
eda-for-python/
├── pyproject.toml
├── uv.lock
├── _quarto.yml
├── index.qmd
├── .github/workflows/publish.yml
└── .gitignore
```
