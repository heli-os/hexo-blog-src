---
title: "[자율 공부방] 학습(작업) 내용 공유 - 17"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2020-09-21 23:50:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2020년 09월 21일 월요일
* 내용: 교과목 파이썬(2) 강의를 듣고 관련 내용을 정리하며 학습하고, 컴퓨터정보과 프로젝트 모임 구성원 상담을 진행했습니다.

# 교과 학습 - 파이썬(2)
## 인터닝(Interning)
> 중복되는 값을 새로운 메모리에 할당하지 않고, 기존 메모리에서 가져오는 행위
* 파이썬은 크기가 작은 객체들을 인터닝(interning)한다.
* 리스트와 같은 변경 가능한 객체는 인터닝하지 않는다.

## 변경가능한 객체를 복사하는 명령
* list()함수 사용
* copy() 함수 사용
* sorted() 함수 사용

## 정렬 함수의 차이
* sort(): 원본 자체가 정렬됨.
* sorted(): 원본은 유지하고 정렬된 결과를 담은 새로운 리스트 객체를 생성하여 반환함.

## 변경 가능한 객체에 대한 iteration
* Dictionary는 에러 발생, List는 에러가 발생하지는 않지만 의도치 않은 결과 발생
* 원본을 복사하고, 복사된 객체를 iteration하는 것이 가장 현명하다.

## string.punctuation
모든 구두점을 담고 있는 String Object (31line in string.py)
[https://github.com/python/cpython/blob/919f0bc8c904d3aa13eedb2dd1fe9c6b0555a591/Lib/string.py#L31](https://github.com/python/cpython/blob/919f0bc8c904d3aa13eedb2dd1fe9c6b0555a591/Lib/string.py#L31)

## 한글 파일 open 시 발생하는 오류
* UnicodeDecodeError: … multibyte sequence  
    ANSI와 UTF-8간에 인코딩 불일치로 인한 오류, file open 시 encoding=”UTF-8” 추가로 해결

# 컴퓨터정보과 프로젝트 모임
* 구성원 상담: 2명
* 다음 예정: 화요일 1명, 목요일 3명 상담