---
layout: post
title: 'webpack 5 module federation'
description:
headline:
modified: 2022-11-25
category: software platform
imagefeature:
tags: [webpack 5 module federation]
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
-   [개념](#개념)

## 개념

### 

-   [https://donggov.tistory.com/196](https://donggov.tistory.com/196)

```JavaScript
$ vue create app    -- 메인 모듈
$ vue create menu   -- 메뉴 모듈
$ vue create basket -- 장바구니 모듈
```

### Module Federation 및 remote/host 설정
```JavaScript
publicPath: "http://localhost:8000",
chainWebpack: (config) => {
  config.optimization.delete("splitChunks");
  config.plugin("module-federation-plugin").use(require("webpack").container.ModuleFederationPlugin, [
    {
      name: "main",
      remotes: {
        menu: "menu@http://localhost:8001/remoteEntry.js",
        basket: "basket@http://localhost:8002/remoteEntry.js",
      },
      shared: require("./package.json").dependencies,
    },
  ]);
},


// menu
publicPath: "http://localhost:8001",
chainWebpack: (config) => {
  config.optimization.delete("splitChunks");
  config.plugin("module-federation-plugin").use(require("webpack").container.ModuleFederationPlugin, [
    {
      name: "menu",
      filename: "remoteEntry.js",
      exposes: {
        "./Chicken": "./src/components/Chicken.vue",
      },
      shared: require("./package.json").dependencies,
    },
  ]);
},

// basket
publicPath: "http://localhost:8002",
chainWebpack: (config) => {
  config.optimization.delete("splitChunks");
  config.plugin("module-federation-plugin").use(require("webpack").container.ModuleFederationPlugin, [
    {
      name: "basket",
      filename: "remoteEntry.js",
      exposes: {
        "./Basket": "./src/components/Basket.vue",
      },
      shared: require("./package.json").dependencies,
    },
  ]);
},

```





### Vuex 설정 및 스토어 공유
```JavaScript
 config.plugin("module-federation-plugin").use(require("webpack").container.ModuleFederationPlugin, [
  {
    name: "main",
    filename: "remoteEntry.js",
    remotes: {
      menu: "menu@http://localhost:8001/remoteEntry.js",
      basket: "basket@http://localhost:8002/remoteEntry.js",
    },
    exposes: {
      "./Store": "./src/store/modules/basket",
    },
    shared: require("./package.json").dependencies,
  },
]);

```