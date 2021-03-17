---
title: "[자율 공부방] 학습(작업) 내용 공유 - 24"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2021-03-17 22:10:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2021년 03월 17일 수요일
* 내용
    * 교과목 웹앱개발, 융합스프링프레임워크 강의를 듣고 관련 내용을 정리하며 학습했습니다.
    * 새로 구매한 맥북 세팅으로 인해 공부는 조금만..

# 웹앱개발
## 뷰포트(viewport)

* 각 장치의 뷰포트 적용 방식에 따라 같은 HTML5 문서가 실행 장치에 따라 다르게 보임
* 레이아웃 뷰포트(Layout viewport)
    * 장치의 전체 화면 해상도에 해당하는 영역
    * 현재 보여지는 브라우저 창의 크기와는 관련이 없음
* 비주얼 뷰포트(visual viewport)
    * 전체 페이지 중에서 현재 화면에 보이는 영역
    * 비주얼 뷰포트의 크기는 레이아웃 뷰포트보다 클 수는 없기 때문에 레이아웃 뷰포트의 크기 즉, 전체 화면의 해상도에 맞게 글자 크기를 표시함

## 미디어 쿼리(Media Query)

* 미디어 유형과 특정 미디어 기능의 조건을 평가하는 논리적 표현식
* 반응형 웹(responsive web) 지원
  사용 장치의 화면 크기에 따라 다른 스타일시트를 적용하는 웹 방식
* 화면 너비와 높이, 화면 비율, 기기 특성 등을 이용한 맞춤형 페이지 구성 가능

### 미디어 쿼리 속성

* 미디어 쿼리를 작성할 때 조건을 명세하기 위해 사용

* 조건식은 쿼리 연산자와 미디어 쿼리 속성으로 구성

* 미디어 쿼리의 기본구조

  ```css
  @media [only 또는 not] 미디어타입 [and (조건)] [and (조건)] ... , [only 또는 not] 미디어타입 [and (조건)]
  ```

| 미디어 쿼리 속성                                    | 의미                                                         |
| --------------------------------------------------- | ------------------------------------------------------------ |
| width  min-width, max-width                         | 웹 페이지의 가로 너비  웹 페이지의 최소 너비, 최대  너비     |
| height  min-height, max-height                      | 웹 페이지의 세로 높이  웹 페이지의 최소 높이, 최대  높이  (screen: 스크롤포함  전체 문서 높이, print: 페이지  높이) |
| device-width  min-device-width, max-device-width    | 장치의 물리적 가로(해상도) 너비  장치의 최소 너비,  최대 너비 |
| device-height  min-device-height, max-device-height | 장치의 물리적 세로(해상도) 높이  장치의 최소 높이,  최대 높이 |
| orientation                                         | 장치 화면 회전 상태  portrait(세로모드; width값이 height보다  작을 경우)  landscape(가로모드;  width값이  height보다 클 경우) |
| aspect-ratio  min-aspect-ratio, max-aspect-ratio    | 화면 비율(너비/높이)  예:  1, 1/1, 16/9, 1280/720  최소 화면 비율,  최대 화면 비율 |
| color  min-color, max-color                         | 색상당 비트수(흑백기기는  0)  색상당 최소 비트수, 최대  비트수 |
| color-index  min-color-index, max-color-index       | 색상수  최소 색상수,  최대 색상수                            |
| monochrome  min-monochrome, max-monochrome          | 흑백기기의 픽셀당 비트수(컬러기기는 0)  흑백기기의 최소 픽셀당 비트수, 최대  픽셀당 비트수 |
| resolution  min-resolution, max-resolution          | 장치의 해상도(dpi)  장치의 최소 해상도, 최대  해상도         |
| scan                                                | TV 스캔  방식(progressive, interlace)                        |

# 융합스프링프레임워크
Spring: IOC, DI, AOP

## Spring Framework의 장점

* 개발을 편리하게 도와주는 추상화가 프레임워크 차원에서 잘 구현되어 있다

## 스프링 IOC

| 구현 클래스                  | 기능                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| GenericXmlApplicationContext | 파일 시스템이나 클래스 경로에 있는 XML 설정 파일을 로딩하여 구동하는 컨테이너 |
| XmlWebApplicationContext     | 웹 기반의 스프링 애플리케이션을 개발할 때 사용하는 컨테이너  |

### 스프링 XML

* Beans: XML 설정파일의 루트 엘리먼트 (`필수`)
* Import: 외부 xml을 불러오고자할 때 사용하는 엘리먼트
* Bean: 스프링에 클래스 등록
    * Id 속성은 생략가능. class 속성 필수
        * id는 유일한 객체값이어야 한다.
        * 자바의 식별자 구성의 규칙을 따른다.
        * 오류예시
          `id="7userService"`: 숫자로 시작
          `id="user service"`: 공백 포함
          `id="user#service"` : 특수 기호 사용
    * 특수기호가 포함될 경우 id 대신 name 속성 사용

### Bean 속성

* Init-method 속성: 멤버변수 초기화 작업이 필요할 때 호출
  <img src="/images/post_include/daily_self-study/image-20210317160441532.png" alt="image-20210317160441532" style="zoom:50%;" />
* Destory-method 속성: 컨테이너가 객체를 삭제하기 직전 호출
  <img src="/images/post_include/daily_self-study/image-20210317160450096.png" alt="image-20210317160450096" style="zoom:50%;" />
* lay-init 속성: <bean>을 미리생성하지 않고 클라이언트가 요청하는 시점에 생성하는 방법. 메모리 관리를 효율적으로 함
  <img src="/images/post_include/daily_self-study/image-20210317160523344.png" alt="image-20210317160523344" style="zoom:50%;" />
* Scope 속성: 클래스로부터 객체의 생성 속성을  말함
  
  <img src="/images/post_include/daily_self-study/image-20210317160541354.png" alt="image-20210317160541354" style="zoom:50%;" />
  
    * singleton: 객체를 한 개만 생성
    * prototype: 객체를 요청할때마다 생성

## 의존성주입(DI)

* 객체간 의존관계를 스프링 설정파일에 등록된 정보를 바탕으로 컨테이너 자동으로 처리해주는방식
* 의존성 설정을 바꾸고 싶을때 프로그램코드를 수정하지 않고 스프링 설정 파일 수정만으로 변경사항을 적용가능

### 방법
* 생성자 인젝션(Constructor Injection)
    ```xml
    <bean id=".." class="..">
        <constructor ref="..."/>
        <constructor value="..."/>
    </bean>
    ```
* 세터 인젝션(Setter Injection): Property로 값 대입
    ```xml
    <bean id=".." class="..">
        <property name=".." ref=".."/>
        <property name=".." value=".."/>
    </bean>
    ```
* P 네임스페이스 이용: `xmlns:p="http://www.springframework.org/scheme/p"`
    * P:변수명-ref="참조할 객체의 이름이나 아이디
    * P:변수명="설정할 값"