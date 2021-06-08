---
layout: post
title: "CocoaPods"
description: 
headline: 
modified: 2021-06-08
category: webdevelopment
imagefeature: cover3.jpg
tags: [CocoaPods]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- 라이브러리 의존성 관리 매니저이고 수많은 xcode 프로젝트 라이브러리들이 cocoapods으로 관리되어진다.
안드로이드에서의 gradle과 같은 역할을 해준다고 보면 생각하기 쉽다.
ios/mac app개발시 필수적으로 널리 이용되고있다.

## 시작

```JavaScript
sudo gem install cocoapods


//Podfile
platform :ios, '8.0'
use_frameworks!

target 'MyApp' do
  pod 'AFNetworking', '~> 2.6'
  pod 'ORStackView', '~> 3.0'
  pod 'SwiftyJSON', '~> 2.3'
end


Pod init


pod install


pod update

```
