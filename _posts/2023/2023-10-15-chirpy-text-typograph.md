---
title: Chirpy Theme에서 사용하는 마크다운 문법을 알아보자
date: 2023-10-15 16:39
categories: hobby
tags:
  - jekyll
  - chirpy
---

자세한 내용은 Chirpy Theme 공식 사이트에서 제공하는 [가이드](https://chirpy.cotes.page/posts/text-and-typography/)를 참고하자.

## 해더

```markdown
# H1 - heading
```
# H1 - heading
{: data-toc-skip='' .mt-4 .mb-0 }

```markdown
# H2 - heading
```
## H2 - heading
{: data-toc-skip='' .mt-4 .mb-0 }

```markdown
# H3 - heading
```
### H3 - heading
{: data-toc-skip='' .mt-4 .mb-0 }

```markdown
# H4 - heading
```
#### H4 - heading
{: data-toc-skip='' .mt-4 }


## 리스트

### 순서가 있는 목록

```markdown
Ordered list

1. 첫번째
	1. 첫번째 - 1
	2. 첫번째 - 2
2. 두번째
3. 세번째
```

1. 첫번째
	1. 첫번째 - 1
	2. 첫번째 - 2
2. 두번째
3. 세번째

### 순서가 없는 목록

```markdown
Unordered list

- 사과
	- 부사
	- 홍옥
- 감
	- 단감
	- 대봉
```

- 사과
	- 부사
	- 홍옥
- 감
	- 단감
	- 대봉

### 할 일 목록

```markdown
- [ ] 할일 목록
	- [x] 우유 사기
	- [ ] 전기세 납부
```

- [ ] 할일 목록
	- [x] 우유 사기
	- [ ] 전기세 납부

### 설명 목록

```
오전
: 오전 또는 상오로 0시부터 12시까지 시간이다.

오후
: 오후 또는 하오로 12시부터 24시까지 시간이다.
```

오전
: 오전 또는 상오로 0시부터 12시까지 시간이다.

오후
: 오후 또는 하오로 12시부터 24시까지 시간이다.

## 인용문

```
> 인용문 예제입니다.
```

> 인용문 예제입니다.

## 프롬프트

마크다운에서는 `callout` 문법이다. 

```
> An example showing the `tip` type prompt.
{: .prompt-tip }

> An example showing the `info` type prompt.
{: .prompt-info }

> An example showing the `warning` type prompt.
{: .prompt-warning }

> An example showing the `danger` type prompt.
{: .prompt-danger }
```

> An example showing the `tip` type prompt.
{: .prompt-tip }

> An example showing the `info` type prompt.
{: .prompt-info }

> An example showing the `warning` type prompt.
{: .prompt-warning }

> An example showing the `danger` type prompt.
{: .prompt-danger }

## 표

```
| Company                      | Contact          | Country |
|:-----------------------------|:-----------------|--------:|
| Alfreds Futterkiste          | Maria Anders     | Germany |
| Island Trading               | Helen Bennett    | UK      |
| Magazzini Alimentari Riuniti | Giovanni Rovelli | Italy   |
```

| Company                      | Contact          | Country |
|:-----------------------------|:-----------------|--------:|
| Alfreds Futterkiste          | Maria Anders     | Germany |
| Island Trading               | Helen Bennett    | UK      |
| Magazzini Alimentari Riuniti | Giovanni Rovelli | Italy   |

## 링크

```
<http://127.0.0.1:4000>
```

<http://127.0.0.1:4000>

## 각주

```
첫 번째 각주[^footnote1]이고, 이건 두번째 각주[^footnote2]이다..
```

첫 번째 각주[^footnote1]이고, 이건 두번째 각주[^footnote2]이다.

## 인라인 코드

```
`1+2` = `3`이다. 
```

`1+2` = `3`이다.

## 이미지

```
![Desktop View](https://chirpy-img.netlify.app/posts/20190808/mockup.png){: width="972" height="589" }
_Full screen width and center alignment_
```

![Desktop View](https://chirpy-img.netlify.app/posts/20190808/mockup.png){: width="972" height="589" }
_Full screen width and center alignment_


## 코드 블록

<pre>
```
코드 블록 예제입니다.
```
</pre>

```
코드 블록 예제입니다.
```


## 각주 

[^footnote1]: 첫 번째 각주
[^footnote2]: 두 번째 각주
