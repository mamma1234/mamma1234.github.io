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

### 장점

-   CSS를 작성하지 않고 인터페이스를 구축할 수 있게 해준다.

기존에는 CSS 파일로 가서 다음처럼 코드를 작성했어야 했다.

```JavaScript
.text {
    font-size: 1.125rem;
    line-height: 1.75rem;
}
```

Tailwind CSS에서는 HTML class 속성에 text-lg만을 넣어주는 것으로 간단하게 스타일을 적용할 수 있다.
예를 들자면- 순수 css에서 작성할때, 배경 그래디언트를 넣을때는 예시로 이정도 용량의 코드를 넣어야 했다.

```JavaScript
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
```

로 해야 했던것을

```JavaScript
<body>
     <div class="bg-gradient-to-r from-yellow-400 to-red-400"></div>
</body>
```

이렇게 할 수 있다.  
div나 다른 태그의 class 부분에 tailwindcss 구문을 넣으면 된다.

### 단점

-   최적화 도구가 없으면 CSS 사이즈가 너무 크다. 유틸리티 우선 CSS의 특성상, 스타일을 사전 지정한 속성들이 모두 담겨있기 때문에 파일 크기가 큰 편이다. v2 기준 minify를 한 CDN 버전이 2.8MB에 육박할 정도. Brotli 압축을 해도 최소한 70kb는 나간다. Tailwind 측에서도 이러한 문제점을 해결하기 위해 빌드 프로세스에서 필요한 스타일만 남기는 기능인 purge의 사용을 권장하고, CDN 사용을 지양, PostCSS 플러그인으로 사용하는 것을 권장하고 있다. 여기서 minify까지 돌리면 10~20kb까지 줄일 수 있다.
