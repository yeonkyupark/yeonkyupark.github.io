---
title: Chirpy theme에서 이미지 테두리 만들기 
date: 2025-03-16
categories: hobby
tags: 
  - chirpy
image: /assets/images/logo_chirpy.png
toc: true
pin: false
math: true
mermaid: true
description: chirpy theme 이미지 image 테두리 border 만들기
---

## Chirpy theme에서 이미지 테두리 만들기

블로그 작성 시 이미지는 원본 상태에서 크기만 조절되어 화면에 표시된다. 이미지 가장자리가 흰색이거나 배경색과 이미지 간 이질감이 있어 경계를 줘야 할 경우 테두리를 넣으면 가독성이 좋아진다.

![테두리가 없는 경우](/assets/images/2025-03-16-image-border-1.png)

필요에 따라 테두리를 만들 수 있도록 css에 기능을 구현하여 사용한다.

### scss 파일 수정

Chirpy theme 7.x 기준으로 다음 경로에 있는 scss 파일을 수정한다.

- `assets/css/jekyll-theme-chirpy.scss`

```css
/* 이미지에 테두리 넣기 */
.img-bordered {
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px;
}
```

두께 1px, 모서리는 4px 수준으로 둥글게 처리한 코드이다.

### 이미지 적용

테두리가 필요한 이미지에 `.img-bordered` id를 추가한다.

```
![테투리가 없는 이미지](images.png)

![테투리가 있는 이미지](images.png){: .img-bordered}

```

위 예제 이미지에 테두리를 추가하면 아래와 같이 표시된다. 시각적으로 보다 편안해 보인다.

![테두리를 만든 경우](/assets/images/2025-03-16-image-border.png)


