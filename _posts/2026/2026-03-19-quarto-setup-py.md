---
title: Quarto에서 각 qmd 파일에 적용할 공통 함수 작성하기
date: 2026-03-19
categories: [hobby]
tags: [quarto]
image: /assets/images/logo_quarto.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

Quarto에서 각 `.qmd` 파일은 서로 독립된 실행 환경에서 렌더링 된다. 따라서 특정 `.qmd` 파일에서 작성한 내용은 다른 파일로 자동으로 이어지지 않는다. 이는 적재한 데이터셋이나 중간 산출된 데이터를 다른 파일에서 사용하기 위해서는 다시 수행하는 번거로움이 발생한다. 이런 경우 공통 함수를 작성하면 수고를 덜 수 있다.

## 공통 함수 작성

초기화나 자주 사용하는 코드를 함수로 작성하여 필요에 따라 호출하여 사용한다.

*setup.py*:

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# 시각화 환경 설정
def initialize_environment(font="Malgun Gothic"):
    # 1. 시각화 스타일
    sns.set(style="whitegrid")

    # 2. 폰트 설정
    plt.rcParams['font.family'] = font

    # 3. 마이너스 깨짐 방지
    plt.rcParams['axes.unicode_minus'] = False

# 데이터 적재
def load_penguins():
    df = sns.load_dataset("penguins")
    return df

# 공통 초기화 함
def setup_all(font="Malgun Gothic"):
    initialize_environment(font)
    df = load_penguins()
    return df
```

## 각 qmd 함수에서 호출

qmd 파일 작성시 호출한다.

*각 qmd 파일*:

```python
from setup import setup_all

df = setup_all()
df.head()
```





