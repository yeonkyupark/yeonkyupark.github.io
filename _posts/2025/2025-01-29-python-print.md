---
title: Python print 
date: 2025-01-29
categories: interest
tags: 
  - python
image: /assets/images/logo_python.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

## Python에서 print() 함수 사용하기

### 문법

```python
print(*objects, sep=' ', end='\n', file=None, flush=False)
```

함수 인자로 사용하는 객체(object)는 모두 문자열로 처리된다. 내부적으로 `str()` 함수로 변환하여 출력하는 형태이다. `sep` 옵션은 객체간 연결 기호를 정의하고, `end` 옵션은 출력할 문자열 마지막 기호를 정의한다.

```python
>>> print("Hello" "World")
HelloWorld
>>> print("Hello World")
Hello World
>>> print("Hello", "World")
Hello World
>>> print("Hello", "World", sep="")
HelloWorld
>>> print("Hello", "World", sep=" ")
Hello World
>>> 
>>> print("Hello", end = " ")
Hello >>> print("World")
World
>>> 
>>> print(1234)
1234
>>> print(str(1234))
1234
>>> 
```

## 출력 포멧

### 문자열 형식 지정자 사용하기

| 형식 지정자 | 설명 |
|------------|----------------|
| `%s` | 문자열(String) |
| `%d` | 정수(Integer) |
| `%f` | 부동소수점(Float) |
| `%x` | 16진수(Hexadecimal) |

하지만 최신 파이썬에서는 **`f-string`**(`f"..."`)이나 **`str.format()`**을 사용하는 것이 더 권장된다.

```python
>>> name = "Alice"
>>> age = 20
>>> print("%s's age is %d." % (name, age))
Alice's age is 20.
>>> 
```

### format() 함수 사용하기

```python
>>> name = "Alice"
>>> age = 20
>>> print("{0}'s age is {1}.".format(name, age))
Alice's age is 20.
>>> 
```

### f문자열 사용하기

```python
>>> name = "Alice"
>>> age = 20
>>> print(f"{name}'s age is {age}.")
Alice's age is 20.
```

## 참고자료

1. https://docs.python.org/3.13/library/functions.html#print 
1. https://wikidocs.net/20403
1. https://wikidocs.net/164969


