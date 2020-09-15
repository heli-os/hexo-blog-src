---
title: "[자율 공부방] 학습(작업) 내용 공유 - 12"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2020-09-16 02:10:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2020년 09월 15일 화요일
* 내용: 교과목 안드로이드(1), 자바프로그래밍(2) 강의를 듣고 관련 내용을 정리하며 학습하고, 코드포코리아 메인테이너 회의를 했습니다.

# 교과 학습 - 안드로이드(1)
## layout_gravity 속성
부모 컨테이너(레이아웃)에 뷰(컨트롤)가 채워지지 않아 여유 공간안에서 뷰를 정렬하는 목적으로 사용. layout_width, layout_height 속성이 match_parent라면 이미 꽉 차 있기 때문에 사용할 수 없다. 

## gravity 속성
뷰(컨트롤)에서 화면에 표시하는 내용물을 정렬하는 목적으로 사용. (TextBox의 내부 Text, ImageView의 내부 Image 등)

## layout_ 으로 시작하는 속성
* Linear, Constraints 등 특정 레이아웃 객체에 특화된 기능을 제공한다.
* 내가 사용하지 않는 레이아웃에 대한 속성은 불필요하므로 메모리의 효율적 관리를 위해 별도로 분리되어 있다.
* 이러한 속성을 소스코드로 제어할 때는 LayoutParams로 설정한다.

## @+id/button, @id/button 의 차이점
* @+id/button: id를 새롭게 생성해서 참조
* @id/button: 기존에 있는 id를 참조

## LinearLayout 속성
### layout_weight
* 남아있는 여유 공간을 얼마나 차지할 수 있는지 비율로 지정하는 속성
* wrap_content 또는 특정 숫자 값으로 지정되어 있어야 한다.

### orientation 속성에 따른 유의사항
* orientation="horizontal" 에서는 위젯(컨트롤)의 layout_width 속성 값에 주의해야 한다.
* orientation="vertical" 에서는 위젯(컨트롤)의 layout_height 속성 값에 주의해야 한다.

## 레이아웃의 중첩
* 전체 레이아웃에서 각 그룹이 서로 다른 방식(방향 등)으로 구성되어야 할 때 레이아웃의 중첩이 필요하다.
* 중첩 레이아웃을 설계할 때에는 전체 레이아웃 구조를 그룹별로 파악하고, 그룹마다 레이아웃을 어떻게 설정할 것인지 단게별로 파악하고 화면을 구성하는 것이 중요하다.

## RelativeLayout
* Linear Layout에 비해 뷰의 배치가 자유롭다.
* 다른 뷰나 부모 뷰와의 상대적인 위치를 이용해 뷰를 배치한다. (Constraints와 유사)
* 기준을 정하지 않고 뷰를 배치하는 경우 top-right에 겹쳐서 배치가 되며, 해상도에 따라 위치가 상대적으로 변한다. (Constraints와 다름)

## FrameLayout
* RelativeLayout과 같이 다른 위젯들을 겹칠 수 있다. 
* 상대적 위치를 사용하는 속성(멤버 필드)가 없어서 메모리 절약 차원에서 유리하다

## TableLayout
* TableRow로 이루어져 있다.
* TableRow의 내부에는 위젯이 올 수 있으며, 위젯의 개수에 따라 열의 개수가 정해진다.
* 내부 위젯들은 보이지 않는 cell을 부모로 잡기 때문에 match_parent로 TableRow 전체를 채울 수 없다.
* layout_span 속성으로 열을 병합할 수 있다. 

# 교과 학습 - 자바프로그래밍(2)
* abstract class, interface 복습

### instanceof 연산자
* 레퍼런스가 가리키는 객체의 타입 식별을 위해 사용
```java
ObjectName instanceof ClassName
```