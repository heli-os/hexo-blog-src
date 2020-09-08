---
title: "[자율 공부방] 학습(작업) 내용 공유 - 05"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2020-09-08 23:28:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

* 날짜: 2020년 09월 08일 화요일
* 내용: 교과목 안드로이드(1), 자바프로그래밍(2) 강의를 듣고 관련 내용을 정리하며 학습 했습니다.

# 교과 학습 - 안드로이드(1)
## manifests 폴더
AndroidManifest.xml 파일이 존재하며 이 파일을 통해 어플리케이션의 설정 값을 변경할 수 있다. 그 외에 activity와 같은 Component들의 클래스명을 정의한다.

## java 폴더
실제 안드로이드 개발에 필요한 java 파일이 존재한다. Activity 클래스들이 이 곳에 저장된다.
   
## res 폴더
어플리케이션이 동작할 때 사용하는 텍스트 문자열, 이미지, 아이콘, 오디오, 동영상 등 레이아웃 관련 요소가 존재하며 안드로이드 앱 빌드 과정에서 이를 객체로 만들어 관리한다.

## 뷰의 개념
* 뷰: 화면에 보이는 버튼, 그림, 텍스트, 에디트, 라디오 버튼, 체크박스 등 흔히 Control이나 Widget이라 불리는 UI 구성 요소
* 뷰 그룹: 뷰를 여러 개 포함하고 있는 것. 이러한 뷰 그룹도 뷰로 구분된다. 이를 컨테이너 뷰라고 부르기도 한다.
* 위젯: 뷰 중에서 일반적인 컨트롤의 역할을 하는 것. 뷰 그룹(=컨테이너 뷰)은 여기에 속하지 않는다.

## 뷰의 크기 속성
layout_wdith(가로 크기 = 너비), layout_height(세로 크기 = 높이) 속성이 있다.

이들은 3가지 유형의 값을 지정할 수 있다.
1. match_parent: 뷰가 속한 뷰 그룹에 남아있는 여유 공간을 뷰로 가득 채움
2. wrap_content: 뷰에 들어 있는 내용물의 크기에 따라 뷰의 크기가 결정됨
3. 크기 값 지정: 크기를 고정된 값으로 직접 지정하고 싶을 때 사용. px 단위와 dp 단위 사용 가능

## dp와 sp
### dp
dpi를 기준으로 계산되는 단위로 160dpi 화면을 기준으로 1dp = 1px이다. 즉 320dpi 화면에서 1dp는 2px이 된다. 그렇기에 여러 해상도에서 원하는 모양으로 레이아웃을 배치할 수 있다.

### sp
디바이스 글꼴 크기에 따라 크기가 변화한다. 안드로이드 설정에서 전체 폰트 크기를 변경하면 그 설정에 영향 받는다.

## 레이아웃의 종류
1. Constraint Layout
2. Linear Layout
3. Relative Layout
4. Frame Layout
5. Table Layout

## ConstraintLayout에서 위젯을 배치하는 방법
1. 위젯 배치 후 parent(layout)에 대해 constraint 설정
2. 위젯 배치 후 다른 요소(widget)에 대해 constraint 설정
3. 위젯과 guideline 배치 후 guideline에 대해 constraint 설정

## Linear Layout
Linear Layout은 orientation 속성이 필수이며 horizontal, vertical을 속성의 값으로 가질 수 있는데 Default는 horizontal이다.

레이아웃에 위젯을 배치할 때에는 orientation 속성의 값에 따라 위젯의 설치 위치가 정해지며 layout_width, layout_height 속성에 match_parent, wrap_content 등의 값을 적용하여 그 크기를 변경할 수 있다.

# 교과 학습 - 자바프로그래밍(2)
## 개요
* 1학기 자바프로그래밍(1) 클래스, 추상클래스, 인터페이스 개념 복습

## 인터페이스의 구성 요소
1. 상수와 추상 메소드
    * public static final 멤버 필드
    * public abstract 멤버 메서드
    * public static 멤버 메서드
   