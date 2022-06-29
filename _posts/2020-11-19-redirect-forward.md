---
layout: post
title: 'Redirect'
description:
headline:
modified: 2020-11-19
category: webdevelopment
imagefeature:
tags: [Redirect Forward]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# 포워딩(Forwarding)

웹 컨테이너(Web Container) 차원에서 페이지 이동만 있는 것이다. 실제로 클라이언트는 다른 페이지로 이동을 했는지 알 수 없다. 그렇기 때문에 웹 브라우저에는 최초에 호출한 URL이 표시되며 이동한 페이지의 URL 정보는 볼 수 없다. 동일한 웹 컨테이너에 있는 페이지로만 이동 할 수 있다.

포워딩은 클라이언트와 통신없이 서버에서만 처리되는 것이기 때문에 리다이렉트보다 나은 성능을 보여준다.

그리고 현재 실행중인 페이지와 Forwarding에 의해 호출될 페이지는 Request와 Response 객체를 공유한다. 객체를 요청에 담고 해당 요청을 사용할 다음 자원에 전송한다는 뜻이다.

간단히 말하여 말 그대로 Forward(건내주기)한다는 것이다. 따라서 사용자가 최초로 요청한 요청정보는 다음 URL에서도 유효한 것이다.

# 리다이렉트(Redirect)

웹 컨테이너(Web Container)는 sendRedirect() 메서드가 호출되어 리다이렉트(Redirect) 명령이 들어오면 웹 브라우저에게 다른 페이지로 이동하라고 명령한다. 이 명령에는 브라우저가 웹 컨테이너의 응답을 받은 후 다시 요청을 보낼 새로운 URL을 포함한다. 그러면 웹 브라우저는 URL을 지시된 주소로 바꾸고 그 주소로 이동한다. 다른 웹 컨테이너에 있는 주소로 이동이 가능하며 새로운 페이지에서는 Request와 Response 객체가 새롭게 생성된다.

리다이렉트는 추가적으로 발생한 처리 때문에 포워딩보다 느리다. 중요한 것은 마지막으로 수행하는 작업은 새로운 요청에 의한 것이고, 이것을 클라이언트가 알고있기 때문에 브라우저창의 주소가 처음 요청한 주소가 아닌 다시 요청을 보낼 새로운 주소값으로 변한다.

간단히 말하여 최초 요청을 받은 첫 번째 URL에서 클라이언트에 Redirect할 두 번째 URL을 리턴하고, 클라이언트는 전혀 새로운 요청을 생성하여 두 번째 URL에 다시 요청을 보낸다. 따라서 처음 보냈던 요청정보는 더이상 유효하지 않는 것이다.

출처: https://sdevstudy.tistory.com/26 [.]
