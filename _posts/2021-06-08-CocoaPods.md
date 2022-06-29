---
layout: post
title: 'CocoaPods'
description:
headline:
modified: 2021-06-08
category: webdevelopment
imagefeature:
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

-   라이브러리 의존성 관리 매니저이고 수많은 xcode 프로젝트 라이브러리들이 cocoapods으로 관리되어진다.
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

### pod install

pod을 프로젝트에 세팅하기 위하여 맨 처음에 사용됩니다. 하지만 Podfile의 pod을 추가, 수정, 삭제할 때에도 사용됩니다.

pod install 명령어를 실행하면 새로운 pod을 다운받고 설치합니다. 그리고 각 pod 마다 설치된 버전을 Podfile.lock 에 기록해 놓습니다. Podfile.lock은 설치된 pod들의 버전을 계속 추적하여 기록해놓고 유지시키는 역할을 합니다.

pod install 을 실행하면,
Podfile.lock에 리스트된 팟들에 대해선 지정된 버전만 다운받습니다. 새로운 버전이 존재하는지 체크하지 않는 것이죠!
Podfile.lock에 리스트되지 않은 팟들은 Podfile에 명시된 버전 조건으로 검색하여 다운로드 받습니다. (ex. pod 'MyPod', '~>1.2')

### pod update

pod update {팟이름} 을 실행시키면, 코코아팟은 해당 팟의 업데이트된 버전이 있는지 검색합니다. Podfile.lock을 참조하지 않죠. 이 명령어는 팟을 최신 버전으로 업데이트 시켜주는 것입니다. (단, Podfile의 버전 조건과 일치해야 합니다.) 단순하게 pod update 만 실행시키면 코코아팟은 모든 팟에 대해 가능한 최신 버전으로 업데이트를 실행합니다.

### pod outdated

pod outdated 를 실행하면, 코코아팟은 Podfile.lock에 리스트된 것보다 새로운 버전을 가진 모든 팟을 나열합니다. 이 팟들에 대해 pod update {팟이름} 을 실행한다면 업데이트가 될 것이라는 것을 의미합니다. (역시나 Podfile의 버전 조건과 부합하는 한!)

### pod repo update

/Users/{사용자이름}/.cocoapods/repos 에 있는 모든 podspec 파일을 업데이트 합니다. podspec 파일에는 해당 pod 의 주소 등 중요한 정보들이 담겨있습니다.

```JavaScript
spec.source = { :git => 'https://github.com/Alamofire/Alamofire.git', :tag => 'v3.1.1' }
```

~/.cocoapods/repos 에는 모든 pod에 대해 가능한 버전들의 podspec 파일들이 모여있습니다. pod repo update 를 실행하게 되면 최신 podspec 파일들로 업데이트되게 되는 것입니다. 추가한 라이브러리에 대한 podspec 이 업데이트되지 않아 오류가 날 경우 이 명령어를 통하여 해결할 수 있습니다.

## Podfile.lock을 커밋하세요!

동료와 같이 협업하고 있다면! 꼭 Podfile.lock을 공유해야 합니다. pod 버전을 모두가 동일하게 쓰도록 유지시키는 역할을 하는 것이죠. 그리고 Podfile이 수정될 일이 생긴다면 pod install 명령어를 통해 의존성을 관리하면 됩니다. 만약 동료들과 같은 CHECKSUM을 얻는데에 실패했다면 간단하게 rm -rf Pods && pod install 을 실행하면 됩니다.
