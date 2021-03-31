---
title: "[자율 공부방] 학습(작업) 내용 공유 - 32"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2021-03-31 23:00:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2021년 03월 31일 수요일
* 내용
    * 교과목 융합스프링프레임워크 강의 수강 후 관련 내용을 정리하며 학습했습니다.
    * LeetCode 문제(206, 2, 24)풀이 일부 진행했습니다.

# 융합스프링프레임워크

## AOP

`Aspect Oriented Programming` 의 약자로 관점 지향 프로그래밍이라고 불린다.

관점 지향은 쉽게 말해 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 보고 그 관점을 기준으로 각각 모듈화하겠다는 것이다.

여기서 모듈화란 어떤 공통된 로직이나 기능을 하나의 단위로 묶는 것을 말한다.

### 조인포인트(Join Point)

* 클라이언트가 호출하는 모든 비즈니스 메소드
* 어드바이스가 적용되는 위치, 대상 / 타겟 객체가 구현한 모든 메소드

### 포인트 컷(Pointcut)

* 필터링 된 비즈니스 메소드 즉, 조인 포인트 중 AOP를 적용시키고자 하는 특정한 메소드 => 핵심관심 메소드
* 어드바이스를 적용할 타겟의 메소드를 정규표현식을 통해 선별

### 어드바이스(Advice)

* 공통적인 기능을 하는 메소드 => 횡단관심 메소드
* 어드바이스는 타겟에 제공할 부가기능을 담고 있다.
* 동작 시점에 따라 5개로 구분할 수 있다.

### 위빙(Weaving)

* 포인트 컷으로 지정한 핵심 관심 메소드(핵심 기능)가 호출될 때 어드바이스(부가 기능)에 해당하는 횡단 관심 메소드가 삽입되는 과정
* AOP가 핵심기능(타겟)의 코드에 영향을 주지 않으면서도 필요한 부가기능(어드바이스)를 추가, 변경할 수 있도록 해주는 핵심적인 처리과정이다.

### 애스팩트(Aspect)

* 애스팩트: 포인트 컷(핵심 기능) + 어드바이스(부가 기능)의 결합
* 포인트 컷 메소드에 따라 어떤 어드바이스 메소드를 실행할 지 결정한다
* AOP의 동작 방식을 결정하는 핵심적인 기본 모듈

# LeetCode

## 206. Reverse Linked List

> Given the `head` of a singly linked list, reverse the list, and return *the reversed list*.

https://github.com/960813/leetcode-problems/commit/51b0dc586f9e7de9ac29f9b5c8e73fed5f04d11f

## 2. Add Two Numbers

> You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.
>
> You may assume the two numbers do not contain any leading zero, except the number 0 itself.

https://github.com/960813/leetcode-problems/commit/d3cfa3e3d01be0c7dc3322ff4de8c7cf79d3277f

## 24. Swap Nodes in Pairs

> Given a linked list, swap every two adjacent nodes and return its head.

https://github.com/960813/leetcode-problems/commit/85c866d32158beb9d61f92f9d1494e7bdda54f5d