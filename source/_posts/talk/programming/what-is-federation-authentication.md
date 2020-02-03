---
title: "타사 인증(Federation Authentication)이란?"
toc: false
tags: [타사 인증,회원 인증,로그인,회원가입]
categories:
  - Talk
  - Programming
date: 2020-01-24 20:54:18
thumbnail: /images/post_include/what-is-federation-authentication_0000.jpg
---
일반적인 서비스는 사용자의 정보를 데이터베이스에 저장하고, 이를 활용하는 방향으로 운영되기에 '회원가입'과 '로그인' 과정이 필수적으로 요구된다.

최근에는 과거로부터 이어진 아이디와 패스워드를 이용한 단순 로그인에서 더 나아가 페이스북/트위터/깃허브/구글/카카오 등 타사의 유저 정보를 이용한 회원가입 및 로그인 서비스 즉, 타사인증(Federation Authentication)을 도입해 사용자의 편의성을 증대시키려는 노력이 계속되고 있다.

<center><img src="/images/post_include/what-is-federation-authentication_0001.png" width="50%" alt="DigitalOcean 회원가입 화면" title="DigitalOcean 회원가입 화면"></center>

타사인증 활용이 증가함에 따라 신규 서비스 개발에서도 타사인증을 지원하려는 경향을 보인다. 하지만 막상 타사 인증을 구현하려고 문서를 찾아보면, 서비스마다 인증 관련 API 사용법이 다르기 때문에 이를 구현하는 것이 힘들 수 있다.

Node.js의 경우 passport-js라는 통합 인증 관리 패키지가 존재하니, 해당 패키지를 활용하여 개발을 진행해보아도 좋을 것이다.

링크 : [[Node.js] passport-js 패키지를 이용한 회원 관리](//blog.jupiterflow.com/2020/01/24/nodejs/modules/passport-js/manual-01/)