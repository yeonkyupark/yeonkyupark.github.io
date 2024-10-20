---
title: 데이터프레임에서 행과 열 추가 및 삭제하기
date: 2024-10-20
categories: Interest
tags:
  - python
  - R
  - wrangling
image: /assets/images/logo_wrangling.png
toc: true
pin: false
math: true
mermaid: true
description: 행과 열로 구성되어 있는 데이터프레임 자료형에 데이터를 삽입과 삭제하는 방법을 알아 본다.
---
## 데이터프레임에서 행과 열 추가 및 삭제하기

### Python

```python
import pandas as pd
import seaborn as sns
penguins = sns.load_dataset('penguins')
df = penguins.copy()
```

#### 행 추가 및 삭제

##### 행 추가

pandas에서 행을 추가하는 방법은 크게 3가지가 있다[^1].

- df.loc 사용
- df.append() 사용
- concat() 사용

**df.loc 사용**

index를 명시적으로 지정하여 행을 추가할 수 있다.

```python
df.loc[[len(df.index)-1]]
```

> | |species|island|bill_length_mm|bill_depth_mm|flipper_length_mm|body_mass_g|sex|
|-|---|---|---|---|---|---|---|
|343|Gentoo|Biscoe|49.9|16.1|213.0|5400.0|Male|

```python
df.loc[len(df.index)] = ['Adelie', 'Torgersen', 39.2, 19.3, 180.2, 8331, 'Male']
df.loc[len(df.index)-2:]
```

> | |species|island|bill_length_mm|bill_depth_mm|flipper_length_mm|body_mass_g|sex|
|-|---|---|---|---|---|---|---|
|343|Gentoo|Biscoe|49.9|16.1|213.0|5400.0|Male|
|344|Adelie|Torgersen|39.2|19.3|180.2|8331.0|Male|

**df.append() 사용**

`append()`[^append] 함수를 사용하여 행을 추가할 수 있다.

```python
df_new = pd.Series(['Adelie', 'Torgersen', 39.2, 19.3, 180.2, 8331, 'Male'], index = df.columns)
df_new
```

	species                 Adelie
	island               Torgersen
	bill_length_mm            39.2
	bill_depth_mm             19.3
	flipper_length_mm        180.2
	body_mass_g               8331
	sex                       Male
	dtype: object

```python
df = df.append(df_new, ignore_index=True)
df.tail()
```

> | |species|island|bill_length_mm|bill_depth_mm|flipper_length_mm|body_mass_g|sex|
|-|---|---|---|---|---|---|---|
|340|Gentoo|Biscoe|46.8|14.3|215.0|4850.0|Female|
|341|Gentoo|Biscoe|50.4|15.7|222.0|5750.0|Male|
|342|Gentoo|Biscoe|45.2|14.8|212.0|5200.0|Female|
|343|Gentoo|Biscoe|49.9|16.1|213.0|5400.0|Male|
|344|Adelie|Torgersen|39.2|19.3|180.2|8331.0|Male|

**concat() 사용**

`concat()`[^concat] 함수를 이용하여 행을 추가할 수 있다.

```python
df_new = pd.DataFrame([['Adelie', 'Torgersen', 39.2, 19.3, 180.2, 8331, 'Male']], columns = df.columns)
pd.concat([df, df_new], ignore_index = True).tail()
```

> | |species|island|bill_length_mm|bill_depth_mm|flipper_length_mm|body_mass_g|sex|
|-|---|---|---|---|---|---|---|
|340|Gentoo|Biscoe|46.8|14.3|215.0|4850.0|Female|
|341|Gentoo|Biscoe|50.4|15.7|222.0|5750.0|Male|
|342|Gentoo|Biscoe|45.2|14.8|212.0|5200.0|Female|
|343|Gentoo|Biscoe|49.9|16.1|213.0|5400.0|Male|
|344|Adelie|Torgersen|39.2|19.3|180.2|8331.0|Male|

##### 행 삭제

#### 열 추가 및 삭제

##### 열 추가

##### 열 삭제



### R

#### 행 추가 및 삭제

##### 행 추가

##### 행 삭제

#### 열 추가 및 삭제

##### 열 추가

##### 열 삭제


## 참고자료
[^1]: [How to add one row in an existing Pandas DataFrame?](https://www.geeksforgeeks.org/how-to-add-one-row-in-an-existing-pandas-dataframe/)

[^append]: [pandas.DataFrame.append](https://pandas.pydata.org/pandas-docs/version/1.4/reference/api/pandas.DataFrame.append.html)

[^concat]: [pandas.concat](https://pandas.pydata.org/pandas-docs/version/1.4/reference/api/pandas.concat.html?highlight=concat#pandas.concat)