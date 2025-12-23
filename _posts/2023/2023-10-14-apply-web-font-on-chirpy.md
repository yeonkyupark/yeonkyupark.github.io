---
title: Chirpy Theme에 web font를 적용해 보자
date: 2023-10-14 21:56
categories: hobby
tags:
  - jekyll
  - chirpy
---

## 웹 폰트 구하기
웹 폰트는 [구글폰트](https://fonts.google.com/?subset=korean)를 사용한다. 사용할 폰트는 국민폰트라 볼 수 있는 Noto Sans Korean Regular 400을 기준으로 한다.

![image](https://github.com/yeonkyupark/yeonkyupark.github.io/assets/72383349/1adada3b-40e9-4bc0-9794-db48040612e7)


화살표가 가리키는 더하기`(+)` 버턴을 누르면 다음과 같이 사이트에 적용할 수 있는 코드가 나타난다.

![image](https://github.com/yeonkyupark/yeonkyupark.github.io/assets/72383349/e9501150-4b40-47b0-bd4a-6be412f501f4)


폰트를 @import 형태로 적용하므로 라디오 버튼을 변경해 준다.

## 웹 폰트 적용하기

아래 경로에 있는 파일에 웹 폰트를 적용한다.

- `/_sass/addon/commons.scss`{: .filepath}

scss 파일 가장 윗 줄에 위에서 선택한 코드를 복사한다.

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+KR&display=swap');
```

그리고 font-family도 선택한 코드에 맞춰 함께 수정한다.

```css
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

- 변경 전
  ![image](https://github.com/yeonkyupark/yeonkyupark.github.io/assets/72383349/2d614ddb-9252-495f-b087-7b8075c1ad6f)

- 변경 후
  ![image](https://github.com/yeonkyupark/yeonkyupark.github.io/assets/72383349/b846a86d-fc6c-499d-bf33-4fe7973283a0)
  
- 다른 폰트
  ![image](https://github.com/yeonkyupark/yeonkyupark.github.io/assets/72383349/d2ee6ffe-75fa-4559-9c72-c84a6c2e5231)


## 추가 내용

`v6.2.3` 기준 아래 경로 css 파일 변경만으로 웹 폰트 적용이 가능하다.

- `/_sass/addon/variables.scss`{: .filepath}


```css
/* fonts */

/* $font-family-base: 'Source Sans Pro', 'Microsoft Yahei', sans-serif !default; */
font-family-base: 'Noto Sans KR', sans-serif !default;
font-family-heading: Lato, 'Microsoft Yahei', sans-serif !default;
```

