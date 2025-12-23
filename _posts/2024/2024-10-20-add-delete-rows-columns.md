---
title: Python DataFrame에서 행과 열 추가 및 삭제하기
date: 2024-10-20
categories: interest
tags:
  - python
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
|-|-|---|---|---|---|---|---|---|
|340|Gentoo|Biscoe|46.8|14.3|215.0|4850.0|Female|
|341|Gentoo|Biscoe|50.4|15.7|222.0|5750.0|Male|
|342|Gentoo|Biscoe|45.2|14.8|212.0|5200.0|Female|
|343|Gentoo|Biscoe|49.9|16.1|213.0|5400.0|Male|
|344|Adelie|Torgersen|39.2|19.3|180.2|8331.0|Male|

##### 행 삭제

DataFrame에서 데이터를 삭제하는 방법은 `drop()` 함수를 이용하는 것이다[^drop][^drop2].

> *DataFrame.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors=’raise’)*

```python
df.drop(df.index[(1,3), ]).head()
```

> | |species|island|bill_length_mm|bill_depth_mm|flipper_length_mm|body_mass_g|sex|
|-|---|---|---|---|---|---|---|
|0|Adelie|Torgersen|39.1|18.7|181.0|3750.0|Male|
|2|Adelie|Torgersen|40.3|18.0|195.0|3250.0|Female|
|4|Adelie|Torgersen|36.7|19.3|193.0|3450.0|Female|
|5|Adelie|Torgersen|39.3|20.6|190.0|3650.0|Male|
|6|Adelie|Torgersen|38.9|17.8|181.0|3625.0|Female|

```python
df.drop(df.index[100:]).tail()
```

> | |species|island|bill_length_mm|bill_depth_mm|flipper_length_mm|body_mass_g|sex|
|-|---|---|---|---|---|---|---|
|95|Adelie|Dream|40.8|18.9|208.0|4300.0|Male|
|96|Adelie|Dream|38.1|18.6|190.0|3700.0|Female|
|97|Adelie|Dream|40.3|18.5|196.0|4350.0|Male|
|98|Adelie|Dream|33.1|16.1|178.0|2900.0|Female|
|99|Adelie|Dream|43.2|18.5|192.0|4100.0|Male|

```python
df.drop(df[df['species']=='Adelie'].index).head()
```

> | |species|island|bill_length_mm|bill_depth_mm|flipper_length_mm|body_mass_g|sex|
|-|---|---|---|---|---|---|---|---|
|152|Chinstrap|Dream|46.5|17.9|192.0|3500.0|Female|
|153|Chinstrap|Dream|50.0|19.5|196.0|3900.0|Male|
|154|Chinstrap|Dream|51.3|19.2|193.0|3650.0|Male|
|155|Chinstrap|Dream|45.4|18.7|188.0|3525.0|Female|
|156|Chinstrap|Dream|52.7|19.8|197.0|3725.0|Male|


#### 열 추가 및 삭제

##### 열 추가

```python
import pandas as pd
import seaborn as sns
df = sns.load_dataset("penguins")

df.head()
```

> | |species | island | bill_length_mm | bill_depth_mm | flipper_length_mm | body_mass_g | sex
-- | -- | -- | -- | -- | -- | --
| | Adelie | Torgersen | 39.1 | 18.7 | 181.0 | 3750.0 | Male
| | Adelie | Torgersen | 39.5 | 17.4 | 186.0 | 3800.0 | Female
| | Adelie | Torgersen | 40.3 | 18.0 | 195.0 | 3250.0 | Female
| | Adelie | Torgersen | NaN | NaN | NaN | NaN | NaN
| | Adelie | Torgersen | 36.7 | 19.3 | 193.0 | 3450.0 | Female

```python
bill_ratio = df['bill_length_mm']/df['bill_depth_mm']
bill_ratio
```

```
0      2.090909
1      2.270115
2      2.238889
3           NaN
4      1.901554
         ...   
339         NaN
340    3.272727
341    3.210191
342    3.054054
343    3.099379
Length: 344, dtype: float64
```

```python
df['bill_ratio'] = bill_ratio
df.head()
```

> | | species | island | bill_length_mm | bill_depth_mm | flipper_length_mm | body_mass_g | sex | bill_ratio
-- | -- | -- | -- | -- | -- | -- | --
| | Adelie | Torgersen | 39.1 | 18.7 | 181.0 | 3750.0 | Male | 2.090909
| | Adelie | Torgersen | 39.5 | 17.4 | 186.0 | 3800.0 | Female | 2.270115
| | Adelie | Torgersen | 40.3 | 18.0 | 195.0 | 3250.0 | Female | 2.238889
| | Adelie | Torgersen | NaN | NaN | NaN | NaN | NaN | NaN
| | Adelie | Torgersen | 36.7 | 19.3 | 193.0 | 3450.0 | Female | 1.901554

##### 열 삭제

```python
df.drop(columns = ['sex', 'bill_ratio'], inplace=True)
df.head()
```

> | |species | island | bill_length_mm | bill_depth_mm | flipper_length_mm | body_mass_g
-- | -- | -- | -- | -- | --
| | Adelie | Torgersen | 39.1 | 18.7 | 181.0 | 3750.0
| | Adelie | Torgersen | 39.5 | 17.4 | 186.0 | 3800.0
| | Adelie | Torgersen | 40.3 | 18.0 | 195.0 | 3250.0
| | Adelie | Torgersen | NaN | NaN | NaN | NaN
| | Adelie | Torgersen | 36.7 | 19.3 | 193.0 | 3450.0

원본 데이터에 반영이 필요한 경우 `inplace=True` 옵션을 적용한다.


## 참고자료
[^1]: [How to add one row in an existing Pandas DataFrame?](https://www.geeksforgeeks.org/how-to-add-one-row-in-an-existing-pandas-dataframe/)

[^append]: [pandas.DataFrame.append](https://pandas.pydata.org/pandas-docs/version/1.4/reference/api/pandas.DataFrame.append.html)

[^concat]: [pandas.concat](https://pandas.pydata.org/pandas-docs/version/1.4/reference/api/pandas.concat.html?highlight=concat#pandas.concat)
[^drop]: [Delete rows/columns from DataFrame using Pandas.drop()](https://www.geeksforgeeks.org/python-delete-rows-columns-from-dataframe-using-pandas-drop/)
[^drop2]: [Drop a list of rows from a Pandas DataFrame](https://www.geeksforgeeks.org/drop-a-list-of-rows-from-a-pandas-dataframe/?ref=oin_asr2)