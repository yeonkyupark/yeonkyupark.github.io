---
title: Chirpy Theme에 web font를 적용해 보자
author: yk
date: 2023-10-14 21:56
categories: "[Project]"
tags: "[jekyll, chirpy]"
---

## 웹 폰트 구하기

웹 폰트는 [구글폰트](http://fonts.google.com/?subset=korean)를 사용한다. 사용할 폰트는 국민폰트라 볼 수 있는 Noto Sans Korean Regular 400을 기준으로 한다.

![[Pasted image 20231014220534.png]]

화살표가 가리키는 더하기(+) 버턴을 누르면 다음과 같이 사이트에 적용할 수 있는 코드가 나타난다.

![[Pasted image 20231014220908.png]]

폰트를 @import 형태로 적용하므로 라디오 버튼을 변경해 준다.

## 웹 폰트 적용하기

아래 경로에 있는 파일에 웹 폰트를 적용한다.

`/_sass/addon/commons.scss`{: .filepath}

scss 파일 가장 윗 줄에 위에서 선택한 코드를 복사한다.

```
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap');
```

그리고 font-family도 선택한 코드에 맞춰 함께 수정한다.

```
body {
  background: var(--main-bg);
  padding: env(safe-area-inset-top) env(safe-area-inset-right)
    env(safe-area-inset-bottom) env(safe-area-inset-left);
  color: var(--text-color);
  -webkit-font-smoothing: antialiased;
  /*font-family: $font-family-base;*/
  font-family: 'Noto Sans KR', sans-serif;
}
```

반영 후 정상 동작하는지 확인한다.

- **변경 전**
  ![[Pasted image 20231014222918.png]]
  
- **변경 후**
  ![[Pasted image 20231014222934.png]]
  다른 폰트
  ![[Pasted image 20231014223533.png]]

