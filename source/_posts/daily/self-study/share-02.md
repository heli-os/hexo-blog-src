---
title: "[자율 공부방] 학습(작업) 내용 공유 - 02"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2020-09-05 23:27:12
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2020년 09월 05일 토요일
* 내용: 외부 일정으로 인해 학습을 조금만 진행했습니다.

# 영이공 LMS 서포터 개발 및 배포
## 개발 배경
* 비대면 강의에 따른 LMS 시스템 도입
* 제출하지 않은 과제, 학습하지 않은 강의를 확인하려면 모든 과목을 일일이 확인해야 하는 불편함이 있었음.

## 주요 기능
* 학습하지 않은 강의와 과제를 한눈에 볼 수 있게 목록으로 제공

## Buitld With
* Javascript
* Chrome Extension API

## Contat
* e-mail: sun@jupiterflow.com
* download: [https://jupiterflow.com/project/10](https://jupiterflow.com/project/10)
* github: [https://github.com/960813/ync-lms-supporter](https://github.com/960813/ync-lms-supporter)

# JPA
## 기본값 타입
* 자바 기본 타입(int, double)
* 래퍼 클래스(Integer, Long)
* String

## 임베디드 타입(embedded type, 복합 값 타입)
* 새로운 값 타입을 직접 정의할 수 있음
* 주로 기본 값 타입을 모아 만들어서 복합 값 타입이라고도 함
* int, String과 같은 값 타입
* 근무 기간(근무 시작일 + 근무 종료일) / 집 주소(도시 + 도로명 + 우편번호)

### 사용법
* @Embeddable: 값 타입을 정의하는 곳에 표시
* @Embedded: 값 타입을 사용하는 곳에 표시
* 기본 생성자 필수

### 장점
* 재사용
* 높은 응집도
* `Period.isWork()` 처럼 해당 값 타입만 사용하는 의미 있는 메소드 생성 가능
* 임베디드 타입을 포함한 모든 값 타입은, 값 타입을 소유한 엔티티에 생명주기를 의존함

### 임베디드 타입과 테이블 매핑
* 임베디드 타입은 엔티티의 값일 뿐이다.
* 임베디드 타입을 사용하기 전과 후에 매핑하는 테이블은 같음
* 객체와 테입르을 아주 세밀하게(find-grained) 매핑하는 것이 가능
* 잘 설계한 ORM 애플리케이션은 매핑한 테이블의 수보다 클래스의 수가 더 많음

### @AttributeOverride: 속성 재정의
* 한 엔티티에서 같은 값 타입을 사용했을 때 사용
* 컬럼 명이 중복됨
* @AttributeOverrides, @AttributesOverride를 사용해서 컬럼 명 속성을 재정의