---
title: 옵시디언에서 파이썬 코드 실행하기
date: 2026.01.18.
categories: [hobby]
tags: [obsidian]
image: /assets/images/logo_obsidian.png
toc: true
pin: false
math: true
mermaid: true
description: 
---

본 글에서는 옵시디언 환경에서 프로그래밍 실습을 위한 플러그인을 소개한다.

- 플러그인 설치
- 기본 환경 설정
- 주요 기능
- 기능 확장

## 플러그인 설치

이 글에서 필요한 플러그인은 2가지이다.

- excute code
	- https://github.com/twibiral/obsidian-execute-code 
- code styler
	- https://github.com/mayurankv/Obsidian-Code-Styler 

## 기본 환경 설정

먼저 `Excute Code`를 설치한다. 설치가 완료되면 옵션에서 필요한 정보를 설정한다. 참고로, 본 플러그인에서 지원하는 프로그래밍 언어는 JavaScript, Python, R, C/C++, Java, SQL, Latex 외 다양하다. 본 글에서는 Python을 기준으로 설명한다.

![](/assets/images/Pasted%20image%2020260118122912.png)

사용하고자 하는 언어를 선택하다. 그 다음 해당 언어가 설치되어 있는 경로를 설정한다.

## 주요 기능 

### 코드 실행

먼저 아래와 같이 파이썬으로 코드를 작성한다. 다음 읽기 모드에서 보면 옵시디언에서 제공하는 코드블록을 확인할 수 있다.

````python
```python
a = 1
b = 3
print(f'a+b={a+b}')
```
````

![](/assets/images/Pasted%20image%2020260118125925.png)

참고: R언어 경우

````r
```r
a <- 1
b <- 3
cat(sprintf("a+b=%d", a + b))
```
````

`Excute Code` 활성화 후 확인하면 다음과 같이 `Run` 버튼을 확인할 수 있다.

**편집모드**

````python
```python
a = 1
b = 3
print(f'a+b={a+b}')
```
````

**읽기모드**

![](/assets/images/Pasted%20image%2020260118132501.png)

위 이미지는 `Run` 실행 후 결과 화면이다.

편집모드에서도 작성된 코드를 실행하려면 코드블록 기호(\`\`\`) 뒤에 `run-python`을 입력한다.

````python
```run-python
a = 1
b = 3
print(f'a+b={a+b}')
```
````

![](/assets/images/Pasted%20image%2020260118133934.png)

### 공통 코드 작성

모든 코드블록 상단에 특정 코드를 추가할 수 있다. 옵션에 `Insect Python code`에 필요한 추가할 내용을 작성한다.

![](/assets/images/Pasted%20image%2020260118135130.png)

![](/assets/images/Pasted%20image%2020260118135242.png)

## 기능 확장

`Code Styler` 플러그인을 설치하여 코드 실행 외 코드 가독성 및 설명을 위한 기능을 사용할 수 있다.

### 코드블록 기본 동작

![](/assets/images/Pasted%20image%2020260118135719.png)

본 플러기인을 설치하면 코드블록 좌측에 행번호를 확인할 수 있다. 행번호를 기반으로 특정 코드를 하이라이트하여 가독성을 향상할 수 있다.

````python
```python hl:3
a = 1
b = 3
print(f'a+b={a+b}')
```
````

![](/assets/images/Pasted%20image%2020260118140644.png)

하이라이트가 필요한 코드 범위를 `hl:` 기호 뒤에 명시한다. 

- hl: 1
- hl: 1,3
- hl: 2-3

옵션 → `Choose Codeblock Settings` → `Codeblock Highlighting` 메뉴를 통해 하이라이트 색상을 변경하거나 추가할 수 있다.

![](/assets/images/Pasted%20image%2020260118141452.png)

````python
```python hl:3 warn:1 error:2 
a = 1
b = 3
print(f'a+b={a+b}')
```
````

![](/assets/images/Pasted%20image%2020260118141601.png)

### 코드블록 외관 설정

`title`, `icon` 등을 통해 코드블록 가독성을 향상할 수 있다.

```python title='파이썬 예제코드'
a = 1
b = 3
print(f'a+b={a+b}')
```

- title: 코드블록 상단에 제목을 명시
- ref: 참고할 문서를 연결, 예) `ref: [[참고할 문서]]`

`title`과 `ref`가 함께 작성된 경우, 출력은 `title`, 링크는 `ref`로 동작한다. 이 설정은 편집모드에서 동작한다. 읽기모드에서도 동작하려면 `옵선` → `Choose Codeblock Settings` → `Codeblock Header` → `Display Header Language Tag Appearance`, `Display Header Language Icons` → `Always`로 설정한다.



## 참고사항

> **리눅스에서 경로 확인하기**
> python 설치 경로를 확인한다. $PATH에 해당 경로가 설정되어 있다면 파일명만 명시해도 된다.
> 
> ```
> whereis python3
python3: /usr/bin/python3 /usr/lib/python3 /etc/python3 /usr/share/python3 /usr/share/man/man1/python3.1.gz
> ```

