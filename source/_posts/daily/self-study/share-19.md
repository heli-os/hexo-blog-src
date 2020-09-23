---
title: "[자율 공부방] 학습(작업) 내용 공유 - 19"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2020-09-22 23:50:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2020년 09월 22일 화요일
* 내용: 교과목 자바프로그래밍(2), 안드로이드(1) 강의를 듣고 관련 내용을 정리하며 학습했습니다.

# 교과 학습 - 자바프로그래밍(2)
## Wrapper 클래스
* 자바의 기본 타입을 클래스로 만든 8개의 클래스
* 각 타입에 대한 Utility static method를 제공한다.

## Boxing
* 기본 타입 값을 Wrapper 객체로 변환
```java
Integer ten = Integer.valueOf(10);
Integer ten = 10;
```

## UnBoxing
* Wrapper 객체에 들어 있는 기본 타입의 값을 빼내는 것
```java
int n = ten.intValue();
int n = ten;
```

## 난수 발생
* Math 클래스의 random() 메소드 이용
* Random 클래스의 nextInt(n) 등의 메소드 이용

## 날짜 관련 클래스
* Date, Calendar 등

# 교과 학습 - 안드로이드(1)
## BitmapDrawable 객체
* 이미지 파일을 객체화 하는데 사용
* getResources().getDrawable(..) 메소드로 가져온 객체를 BitmapDrawable 로 캐스팅 후 활용 가능
* getIntrinsicWidth(), getIntrinsicHeight(): 비트맵의 원본 크기 반환

## check button / radio button
* Check button: 다수 개의 항목에 다중 선택을 받을 때 사용
* Radio button: 다수 개의 항목 중 단일 선택을 받을 때 사용

## resource 작성 시 유의사항
* 파일명과 폴더명은 영어 소문자, 숫자, 언더바로만 이루어져야 한다.
* 파일명과 폴더명의 시작은 영어 소문자 혹은 언더바여야 한다.

## StateDrawable
* state_pressed: 사용자가 뷰를 누르고 있을 때 설정됨.
* state_checked: 뷰가 현재 check 되어있을 때 설정됨.
* state_selected: 뷰(또는 부모 항목)가 현재 선택 될 때 설정됨.

## ShapeDrawable
* rectangle: 사각형
* oval: 타원
* line: 선
* ring: 도넛형(원에서 가운데가 빈 형태)