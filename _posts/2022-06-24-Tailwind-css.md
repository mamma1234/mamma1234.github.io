---
layout: post
title: 'Tailwind'
description:
headline:
modified: 2022-06-24
category: webdevelopment
imagefeature: cover3.jpg
tags: [Tailwind]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# Record

## 목차

-   [](#)

## 개념

    POST CSS는 우리의 CSS를 조금더 현대적으로 바꿔주는 플러그인이다.
    좀더 풀어 설명하자면 POST CSS 는 JS 플러그인을 사용하여 CSS를 변환시키는 툴 입니다.
    POST CSS 는 언어가아니라 자동으로 신기술 CSS 를 호환가능하도록 변환시켜주는 플러그인일 뿐이다.
    CSS에 문제가없는지 미리 확인해서 에러로그를 준다.
    지금 발전중인 CSS의 현대기술들을 브라우저에 호환되도록 자동 변환해준다.
    PostCSS 자체는 아무 일도 하지 않는다. 다만 다양한 플러그인과, 플러그인을 추가할 수 있는 환경을 제공할 뿐이다.

### reset.css

-   기본 스타일링을 초기화하는 방식이다. 각 태그 별로 유용한 스타일도 모두 지워진다.

### 장점

-   CSS를 작성하지 않고 인터페이스를 구축할 수 있게 해준다. 기존에는 CSS 파일로 가서 다음처럼 코드를 작성했어야 했다.
    .text {
    font-size: 1.125rem;
    line-height: 1.75rem;
    }

Tailwind CSS에서는 HTML class 속성에 text-lg만을 넣어주는 것으로 간단하게 스타일을 적용할 수 있다.
예를 들자면- 순수 css에서 작성할때, 배경 그래디언트를 넣을때는 예시로 이정도 용량의 코드를 넣어야 했다.

<style>
div {
   width: 100%;
   height: 100px;
   margin-bottom: 10px;
}
.jbGrad01 {
   background: linear-gradient( to right, yellow, red, purple, blue );
}
</style>

<body>
     <div class="jbGrad01">to yellow, red</div>
</body>

로 해야 했던것을

<body>
     <div class="bg-gradient-to-r from-yellow-400 to-red-400"></div>
</body>

이렇게 할 수 있다.
div나 다른 태그의 class 부분에 tailwindcss 구문을 넣으면 된다.

### 단점

-   최적화 도구가 없으면 CSS 사이즈가 너무 크다. 유틸리티 우선 CSS의 특성상, 스타일을 사전 지정한 속성들이 모두 담겨있기 때문에 파일 크기가 큰 편이다. v2 기준 minify를 한 CDN 버전이 2.8MB에 육박할 정도. Brotli 압축을 해도 최소한 70kb는 나간다. Tailwind 측에서도 이러한 문제점을 해결하기 위해 빌드 프로세스에서 필요한 스타일만 남기는 기능인 purge의 사용을 권장하고, CDN 사용을 지양, PostCSS 플러그인으로 사용하는 것을 권장하고 있다. 여기서 minify까지 돌리면 10~20kb까지 줄일 수 있다.
