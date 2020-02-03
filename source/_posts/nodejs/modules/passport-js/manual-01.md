---
title: "[Node.js] passport-js 패키지를 이용한 회원 관리 - 01"
toc: false
tags: [node.js,passport-js,타사 인증,회원 인증,로그인,회원가입]
categories:
  - Node.js
  - Modules
date: 2020-01-25 19:37:40
thumbnail: /images/post_include/passport-js-manual-01_0001.jpg
---
이전에 타사인증(Federation Authentication)에 대하여 다룬적이 있다.

링크 : [타사 인증(Federation Authentication)이란?](//blog.jupiterflow.com/2020/01/24/talk/programming/what-is-federation-authentication/)

타사 인증을 구현하려고 인증 관련 매뉴얼을 살펴보면 인증 API 제공 업체마다 사용 방법이 상이하여 소스 코드가 복잡해지거나 유지보수가 어려워질 수 있다.

Node.js에는 이러한 문제점을 해결하고자 등장한 **passport-js**라는 패키지가 존재한다.

# 지원
***

<center><img src="/images/post_include/passport-js-manual-01_0002.png" alt="passport-js 패키지 목록" title="passport-js 패키지 목록"></center>

대표적으로 지원하는 업체는 다음과 같다. 더 많은 정보는 [링크](http://www.passportjs.org/)에서 확인할 수 있다.  
**facebook, google, twitter, github, wechat, instagram, linkedin, slack, kakao, ….**

한국에서 서비스할 경우 페이스북/구글/카카오를 지원하면 폭넓은 사용자를 수용할 수 있을 것이다.

추가로 **passport-js** 패키지는 타사인증만을 지원하는 것은 아니다. **passport-local** 패키지를 이용한다면 아이디-패스워드를 이용한 단순 로그인에 대한 **username, password, hash, salt 및 세션** 관리를 손쉽게 처리할 수 있다. (다만, 이를 구현하는 것은 어려울 수 있다.)

'손쉽게 처리할 수 있지만 구현하는 것은 어렵다 라는 것의 의미'
---
***
> 이는 패스워드에 대한 검증, 세션 관리를 어떻게 구현할지 개발자가 신경 써야 하는 비중이 작아진다는 것이다. (그렇다고 이것들의 중요도가 낮아지는 것은 아니다)   
>더불어 편의를 얻기 위해선 작동 원리에 대한 약간의 암기와 이해를 하고 코드를 작성해야 하는데, 이 과정이 다소 어려울 수 있다.

# 마무리
***

다음편에서는 본격적으로 **passport-local** 패키지의 사용 방법에 대하여 다뤄보겠다.

링크 : [[Node.js] passport-js 패키지를 이용한 회원 관리 - 02](//blog.jupiterflow.com/2020/01/25/nodejs/modules/passport-js/manual-02/)