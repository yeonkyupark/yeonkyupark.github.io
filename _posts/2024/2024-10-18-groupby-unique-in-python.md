---
title: python에서 그룹별 범주 구하기
date: 2024-10-18
categories: interest
tags:
  - python
  - r
image: /assets/images/logo_python.png
toc: true
pin: false
math: true
mermaid: true
description: python에서 그룹별 유일한(unique)한 범주를 구하는 방법을 알아본다.
---

## python에서 그룹별 범주 구하기

`groupby()`와 `unique()` 함수를 통해 그룹별 범주형 컬럼에서 유일한 값을 계산한다.

```python

import pandas as pd
import seaborn as sns
penguins = sns.load_dataset('penguins')

```

```python

df = penguins.copy()
df.groupby(['species'])['island'].unique()

```

	species
	Adelie       [Torgersen, Biscoe, Dream]
	Chinstrap                       [Dream]
	Gentoo                         [Biscoe]
	Name: island, dtype: object

```python
df.groupby(['species'])['island'].nunique()
```

	species
	Adelie       3
	Chinstrap    1
	Gentoo       1
	Name: island, dtype: int64

## R에서 그룹별 범주 구하기

```r
library(dplyr)
df <- palmerpenguins::penguins
df %>% 
  group_by(species) %>% 
  reframe(categories = unique(island))
```

	# A tibble: 5 × 2
	  species   categories
	<fct>     <fct>     
	1 Adelie    Torgersen 
	2 Adelie    Biscoe    
	3 Adelie    Dream     
	4 Chinstrap Dream     
	5 Gentoo    Biscoe 

```r
df %>% 
  group_by(species) %>% 
  reframe(categories = n_distinct(island))
```

	# A tibble: 3 × 2
	  species   categories
	  <fct>          <int>
	1 Adelie             3
	2 Chinstrap          1
	3 Gentoo             1


## Reference
1. [https://pandas.pydata.org/docs/reference/api/pandas.unique.html](https://pandas.pydata.org/docs/reference/api/pandas.unique.html)
