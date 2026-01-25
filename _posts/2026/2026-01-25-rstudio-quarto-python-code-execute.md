---
title: RStudio Quarto 문서에서 파이썬 코드 실행하기
date: 2026-01-25
categories: [hobby]
tags: [rstudio, quarto, python]
image: /assets/images/logo_quarto.png
toc: true
pin: false
math: true
mermaid: true
description: RStudio에서 Quarto 문서 작성 시 파이썬 코드가 실행되도록 환경 설정 절차를 알아 본다.
---

RStudio에서 Quarto 문서 작성 시 파이썬 코드가 실행되도록 관련 환경을 설정한다.

**전제**
- 리눅스 환경
- RStudio, Quarto 설치 완료
- Python, uv 설치 완료

전체 구조는 다음과 같다.

1. `uv`로 가상환경 구성
2. 필요 python 패키지 설치
3. `reticulate` 파이썬 경로 설정
4. 파이썬 코드 실행 확인
5. GitHub Actions 자동 빌드 및 배포 확인

## Quarto 프로젝트 생성

RStudio나 Quarto로 프로젝트를 생성한다. 예제는 Quarto Book 프로젝트로 설명한다.

```sh
mkdir python4da
cd python4da
quarto create-project .
```

## uv 가상환경 구성

`uv` 설치 전이면 아래 명령을 통해 설치한다.

```sh
curl -LsSf https://astral.sh/uv/install.sh | sh
source $HOME/.local/bin/env
```

`uv --version` 명령어로 정상 설치되었는지 확인한다.

가상환경을 생성한다.

```sh
uv venv
```

만약 이전에 가상환경이 생성되어 있다면 아래와 같이 모두 삭제 후 새로 설치한다. 이는 불필요한 환경 충돌을 방지한다.

```sh
rm -rf .venv
```


가상환경이 생성되었다면 가상환경을 활성화하고 파이썬 경로를 확인한다.

```sh
source .venv/bin/activate
which python
```

정상적으로 가상환경이 생성되었다면 파이썬 경로는 아래와 같이 출력된다.

```sh
.../python4da/.venv/bin/python
```

## 필요 패키지 설치

생성된 가상환경에서 필요한 패키지를 설치한다.

```sh
uv pip install pandas palmerpenguins setuptools
```

패키지가 정상적으로 설치되었는지 확인한다. 다음 예제는 `palmerpenguins` 패키지를 설치하고 제공하는 데이터셋 일부를 출력하는 코드이다.

```sh
python -c "from palmerpenguins import load_penguins; print(load_penguins().head())"
```

## reticulate 환경 설정

RStudio Quarto에서 파이썬 코드를 실행하기 위해서는 `reticulate`를 사용한다. `reticulate`는 실행할 파이썬을 선택하는데 가상환경이 아닌 다른 경로에 있는 파이썬을 선택할 수도 있다. 이를 가상환경 경로로 강제 지정한다.

```r
reticulate::use_python(
  "/home/yk/Projects/python4da/.venv/bin/python",
  required = TRUE
)
```

설정한 가상환경에 위치한 파이썬이 정상 설정되었는지 확인한다.

```r
reticulate::py_config()
```

`python: /home/yk/Projects/python4da/.venv/bin/python` 이와 같이 생성한 가상환경으로 경로가 설정되어야 한다.

## Quarto 환경 설정

`_quarto.yml` 파일에 실행할 파이썬 코드를 아래와 같이 지정한다.

```yaml
project:
  type: book

execute:
  python: .venv/bin/python
```

## Quarto 문서에서 점검

Quarto 문서에서 파이썬 경로가 가상환경으로 설정되어 있는지 점검한다.


```python
import sys
sys.executable
```

출력 결과가 `.../python4da/.venv/bin/python` 와 같이 가상환경으로 설정되어 있다면 정상이다.

실제 코드가 정상 실행되는지 확인하다.

```python
from palmerpenguins import load_penguins

df = load_penguins()
df.head()
```

## GitHub Actions 자동 빌드 및 배포

아래는 workflow 파일이다. 

```yaml
name: Render & Deploy Quarto Book

on:
  push:
    branches: [ main ]

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      # Python 버전 고정 (uv가 이 Python을 사용)
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'

      # uv 설치
      - name: Install uv
        run: |
          curl -LsSf https://astral.sh/uv/install.sh | sh
          echo "$HOME/.local/bin" >> $GITHUB_PATH

      # 가상환경 생성 및 패키지 설치
      - name: Create venv & install dependencies
        run: |
          uv venv
          source .venv/bin/activate
          uv pip install --upgrade pip
          uv pip install -r requirements.txt

      - name: Configure git identity
        run: |
          git config --global user.name "github-actions"
          git config --global user.email "github-actions@github.com"

      - name: Ensure gh-pages branch exists
        run: |
          if ! git ls-remote --exit-code --heads origin gh-pages; then
            git checkout --orphan gh-pages
            git rm -rf .
            echo "Initializing gh-pages branch" > index.html
            git add index.html
            git commit -m "Initialize gh-pages"
            git push origin gh-pages
            git checkout main
          fi

      - name: Install Quarto
        uses: quarto-dev/quarto-actions/setup@v2

      # Quarto 렌더링 (uv venv Python 사용)
      - name: Render book
        run: |
          source .venv/bin/activate
          quarto render

      - name: Publish to gh-pages
        uses: quarto-dev/quarto-actions/publish@v2
        with:
          target: gh-pages
```

`uv` 설치와 `requirements.txt`을 이용한 패키지 설치를 추가한다. 여기까지 문제가 없다면 파이썬 코드 실행 결과가 정상적으로 출력된다. 

***E.O.F***
