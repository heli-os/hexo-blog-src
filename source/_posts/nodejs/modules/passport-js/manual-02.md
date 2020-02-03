---
title: "[Node.js] passport-js 패키지를 이용한 회원 관리 - 02"
toc: true
tags: [node.js,passport-js,타사 인증,회원 인증,로그인,회원가입]
categories:
  - Node.js
  - Modules
date: 2020-01-28 00:10:30
thumbnail: /images/post_include/passport-js-manual-01_0001.jpg
---
**passport-js** 패키지는 여러 인증 기법에 대한 패키지 형태의 미들웨어를 지원하며, 이러한 미들웨어 각각을 전략(Strategy)이라고 부른다.

이번 게시글에서는 아이디, 패스워드를 이용한 단순 로그인을 지원하는 **passport-local** 전략의 사용 방법에 대해서 다루어보려고 한다.

# 설치
***
라우팅을 위한 express, 세션 관리를 위한 express-session을 함께 사용하도록 하겠다. 필요한 패키지를 설치해주자.
```javascript
npm install --save express express-session passport passport-local
```

# 코딩
## 패키지 포함
```javascript
const express = require('express');
const session = require('express-session');
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;
```
설치한 패키지를 사용하기 위해 모두 require해준다.

## 패키지 초기화
```javascript
const app = express();
app.use(express.urlencoded({extended: false})) // for parsing application/x-www-form-urlencoded

app.use(session({
    secret: 'A#SFDASD#R$WT$T$T$#WT',
    resave: false,
    saveUninitialized: true
}));

app.use(passport.initialize());
app.use(passport.session());
```
express를 초기화하여 app라는 변수에 담고 POST 데이터를 받아오기 위한 미들웨어, express-session을 사용하기 위한 미들웨어, passport 미들웨어를 각각 설정해 준다.

## 회원 정보 배열 초기화
```javascript
const users = [
    {
        username: 'keriel',
        password: '111111',
        displayName: 'Mr.Keriel'
    }
];
```
passport의 사용법에 대해서만 다루기 위하여 회원 정보를 저장할 데이터베이스나 파일을 사용하기보다 일반 배열을 사용하려고 한다. users라는 배열에 username, password, display Name이라는 key를 가지는 객체를 담아줬다. 각 key는 순서대로 로그인 아이디, 패스워드, 화면에 표시될 이름이다.

## 필수 passport 설정
```javascript
passport.use(new LocalStrategy({
        usernameField: 'username',
        passwordField: 'password'
    },
    (username, password, done) => {
        for (let i = 0; i < users.length; i++) {
            const user = users[i];
            if (username === user.username) {
                console.log('LocalStrategy', user);
                if (password === user.password) {
                    return done(null, user);
                } else {
                    return done(null, false);
                }
            }
        }
        return done(null, false);
    }
));

passport.serializeUser((user, done) => {
    console.log('serializeUser', user);
    done(null, user.username);
});

passport.deserializeUser((id, done) => {
    console.log('deserializeUser', id)
    for (let i = 0; i < users.length; i++) {
        const user = users[i];
        if (id === user.username) {
            return done(null, user);
            // req.user 객체 생성
        }
    }
});
```
총 3개의 코드 블록을 작성했다. 순서대로 다음과 같은 역할을 한다.
1. local 전략을 사용하기 위한 LocalStrategy 미들웨어 설정
2. 각 전략이 정상적으로 작동했을 때 passport 내부적으로 호출되는 메소드(serializeUser)에 대한 설정
3. passport에서 관리하는 session에 접근할 때 passport 내부적으로 호출되는 메소드(deserializeUser)에 대한 설정

# 설명
## LocalStrategy 설정
passport에서 passport-local 미들웨어를 사용하기 위해서 **LocalStrategy** 객체 생성자를 인자로 passport.use메소드를 호출하였다.

**LocalStrategy** 생성자의 첫 번째 인자로 사용된 객체의 usernameField, passwordField라는 key는 username과 password를 가지고 있는 폼 필드가 어떤 폼 필드인지 명시적으로 나타내주기 위하여 사용한다. (기본값은 각각 username, password이다.)

이러한 username과 password는 **LocalStrategy** 생성자의 두 번째 인자로 사용된 콜백 함수의 인자로 사용된다. 이 경우 POST Body가 `{username: 'keriel', passowrd: '111'}` 일 때 콜백 함수의 첫 번째 인자에 'keriel', 두 번째 인자에 '111'이 넘어가게 된다.

콜백 함수 내부에서 로그인을 위한 아이디, 패스워드의 검증을 마쳤다면 세 번째 인자인 done 콜백 함수를 이용해 또 다른 passport 내부 함수를 호출한다.

## LocalStrategy의 done 함수
첫 번째 인자는 에러 여부를 나타낸다. 로그인 성공 시에는 당연히 null이지만 위 코드에서는 로그인에 실패하였다고 특정 에러가 발생하는 것은 아니기에 null을 넘겨주었다.
두 번째 인자는 원하는 작업에 성공했을 때(위의 코드에서는 로그인 성공) return 할 값을 넘겨준다. user 객체의 정보를 활용하기 위해 user 객체 전체를 넘겨줄 것이며, 로그인 실패 시에는 false를 넘겨주도록 하겠다.

## serializeUser 설정
**serializeUser**는 LocalStrategy의 done 함수 두 번째 인자로 false가 아닌 값이 전달되었을 때 호출된다. 그 후 passport로부터 전달받은 user 객체의 username을 `req.user` 세션에 저장한다. (위치 : `req.session.passport.user` / `req.user`로 접근 가능)


## deserializeUser 설정
**deserializeUser**는 req.user에 접근할 때 호출된다. displayName이라는 값을 사용하려는데 우리는 세션에 username만을 저장하였다. 하지만 현재 세션에는 username만 저장되어 있기에 회원 데이터베이스에서 username에 일치하는 객체를 찾아 req.user 객체로 생성해준다. 덕분에 `req.user.displayName`에 접근할 수 있다.


## 회원가입
POST Body로 전달받은 user 정보를 회원 목록에 추가하고 해당 회원 정보로 로그인한다. 단순 회원가입 시뮬레이션을 위해 중복 확인 등 부수적인 작업은 하지 않았다.

## 로그인
예제에서는 로그인과 관련된 라우트가 두 개 존재한다. 첫 번째는 `app.post('/login',..)` 두 번째는 `app.post('/register',...)`이다.

login post 라우트에서 사용한 `passport.authenticate` 메소드는 첫 번째 인자로 어떤 전략을 사용할 것인지 정해준다. 두 번째 인자에서는 성공(실패) 시 리다이렉트 될 Path, 실패 메시지 출력 여부 등의 옵션을 설정하는 객체를 사용한다. local로 지정해주었기 때문에 위에서 설정한 LocalStrategy 콜백이 호출된다. (`passport.authenticate` 메소드는 내부적으로 `passport.login`메소드를 호출한다.)

register post 라우트에서 사용한 `passport.login` 메소드는 첫 번째 인자로 전달된 객체 정보를 세션에 저장하기 위해 사용한다. [방금 회원 가입한 계정이기에 로그인 검증 과정(LocalStrategy 콜백) 생략 후 곧장 `passport.serializeUser` 호출]

# 마무리
**passport**의 local 전략을 사용하는 방법에 대해서 다뤄보았다. 개발자가 직접 호출하여 처리하는 부분보다는 패키지 내부에서 작동하는 로직이 많아 어렵고 헷갈릴 수 있다. passport-local의 작동 순서를 요약하자면 다음과 같다.
1. (`passport.authenticate` 호출 시)  
    LocalStrategy 콜백 호출 => 회원 검증 로직 수행 
2. [ (1) LocalStrategy의 done 함수 인자가 false가 아닐 시, (2) `passport.login` 호출 시]  
    serializeUser 콜백 호출 => 세션에 값 저장(일반적으로 사용자를 구분할 수 있는 id를 사용)
3. (`req.user`에 접근할 때)  
    deserializeUser 콜백 호출 => serializeUser 콜백으로 인해 세션에 저장된 값을 기반으로 req.user 객체 생성 후 클라이언트에게 반환해준다.
    
게시글에 사용한 예제 소스코드는 GitHub에 업로드 해두었습니다.  
링크 : [GitHub 예제 소스코드](https://github.com/JupiterFlow/blog-exam-source/tree/master/20200125_passport-local)