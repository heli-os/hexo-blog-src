---
title: "[자율 공부방] 학습(작업) 내용 공유 - 30"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2021-03-29 23:10:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2021년 03월 29일 월요일
* 내용
    * LeetCode 문제(561, 238, 121, 234, 21)를 풀이했습니다.
    * 교과목 Linux서버실습 강의를 듣고 관련 내용을 정리하며 학습했습니다.

# LeetCode 문제 풀이

### 561. Array Partition I

```
Given an integer array nums of 2n integers, group these integers into n pairs (a1, b1), (a2, b2), ..., (an, bn) such that the sum of min(ai, bi) for all i is maximized. Return the maximized sum.
```

https://github.com/960813/leetcode-problems/tree/main/src/561

### 238. Product of Array Except Self

```
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
```

https://github.com/960813/leetcode-problems/tree/main/src/238

### 121. Best Time to Buy and Sell Stock

```
You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.
```

https://github.com/960813/leetcode-problems/tree/main/src/121

### 234. Palindrome Linked List

```
Given the head of a singly linked list, return true if it is a palindrome.
```

https://github.com/960813/leetcode-problems/tree/main/src/234_1

https://github.com/960813/leetcode-problems/tree/main/src/234_2

### 21. Merge Two Sorted Lists

```
Merge two sorted linked lists and return it as a sorted list. The list should be made by splicing together the nodes of the first two lists.
```

https://github.com/960813/leetcode-problems/tree/main/src/21

# Linux 서버실습 4주차 학습

## 우분투 유저관리

* passwd 파일
  <img src="/images/post_include/daily_self-study/image-20210329135828628.png" alt="image-20210329135828628" style="zoom:50%;" />
  * 리눅스에 있는 사용자 정보가 기록된 파일
  * 사용자는 3가지 종류가 있음
  * root 사용자, 시스템 사용자, 일반 사용자
* shadow 파일
  <img src="/images/post_include/daily_self-study/image-20210329140250991.png" alt="image-20210329140250991" style="zoom:50%;" />
  * 리눅스 사용자의 비밀번호가 기록된 파일
  * 비밀번호는 암호화 되어 있으며 관련된 정보들이 저장되어 있음
* group 파일
  <img src="/images/post_include/daily_self-study/image-20210329141342446.png" alt="image-20210329141342446" style="zoom:50%;" />
  * 리눅스에 있는 그룹 정보가 기록된 파일
* 명령어
  * adduser 유저명: 유저 추가
  * passwd 유저명: 유저 비밀번호 변경
  * userdel 유저명: 유저 삭제
  * groups 유저명: 유저가 속한 그룹을 표시
  * usermod --groups 그룹명 유저명: 그룹에 유저 추가
    * -d: 홈 디렉토리 지정
    * -u: uid 지정
    * -g: gid 지정
    * -G 그룹 지정
    * -s: 기본 쉘 지정
  * groupadd 그룹명: 새로운 그룹 추가
  * groupmod: 기존의 그룹 정보 변경
    * groupmod -n 바꿀그룹명 그룹명
  * gpasswd 그룹명: 그룹 관리를 위한 명령어(그룹의 암호)
  * groupdel 그룹명: 그룹 삭제

## 파일 소유와 허가권

<img src="/images/post_include/daily_self-study/image-20210329145232737.png" alt="image-20210329145232737" style="zoom:50%;" />

* "rw--", "r--", "r--" 3개씩 끊어서 읽음. (r: read, w: write, x: execute)
* 첫 번째 "rw-"는 소유자(User)의 파일접근 권한
* 두 번째 "r--"는 그룹(Groups)의 파일접근 권한
* 세 번째 "r--"는 그 외의 사용자(Other)의 파일접근 권한
* 숫자로도 표시 가능(8진수, 0~7)

### 명령어

* chmod
  * u: 소유자
  * g: 그룹
  * o: 그 이외의 유저
  * a: 모든 유저
* chown: 파일의 소유자를 변경하는 명령어
  * chown 사용자명.그룹명 ... : 파일의 소유자를 변경하는 명령어
  * chown -R 유저명 디렉토리명: 디렉토리의 소유자를 변경하는 명령어
* chgrp: 파일의 소유자 그룹을 변경하는 명령어

## 특수 파일 권한

<img src="/images/post_include/daily_self-study/image-20210329150846711.png" alt="image-20210329150846711" style="zoom:50%;" />

* setuid: root나 root 그룹에 속해있는 파일을 일반 사용자가 임시로 권한을 받아 실행할 수 있도록 하는 명령어
* setgid: setuid와 같은 기능을 가지고 사용자가 아닌 그룹에 해당 권한을 부여하는 명령
* stiky: stiky로 설정된 디렉토리 안에서는 모든 사용자가 파일/디렉토리를 생성할 수 있지만 다른 사용자의 파일을 삭제할 수는 없도록 설정하는 명령어
* stat 명령아: 파일의 세부 정보를 확인
* chmod 명령어를 이용하여 특수 권한 지정
  <img src="/images/post_include/daily_self-study/image-20210329151142929.png" alt="image-20210329151142929" style="zoom: 67%;" />

## 프로세스와 명령어

### 명령어

* ps: 현재 실행중인 프로세스를 화면에 보여주는 명령어
  * ps -ef
    <img src="/images/post_include/daily_self-study/image-20210329155819423.png" alt="image-20210329155819423" style="zoom: 50%;" />

### 프로세스

하드디스크에 저장된 실행코드(프로그램)가 메모리에 로딩되어 활성화된 것

* 부모 프로세스와 자식 프로세스
  * 모든 프로세스는 부모 프로세스를 가지고 있음
  * 부모 프로세스를 없애면 자식 프로세스도 자동으로 없어짐
  * systemd: PID 0
* fork()
  * 유닉스 계열 시스템에서 사용되는 시스템 명령어
  * 지금 실행되고 있는 프로세스가 자신과 똑같은 프로세스를 복제하여 생성
  * 다중 접속 유저 처리를 위해 사용

### 좀비 프로세스(Zombie Process)

작업을 끝낸 프로세스가 종료되지 않고 비정상적으로 남아있는 프로세스

* 좀비 프로세스로 분류되는 경우
  * 종료가 되다만 프로세스
  * 종료 단계에 멈춰 있는 프로세스
  * 비정상적인, 종료되지 않는 프로세스
  * 부모 프로세스가 죽었는데도 남아 있는 자식 프로세스
  * 부모 프로세스가 비정상인 경우
  * 자식 프로세스가 종료되어 사용하는 리소스는 모두 해제된 상태지만, 부모 프로세스가 자식 프로세스의 종료를 확인하지 못한 상태로 커널의 프로세스 테이블에는 관리되고 있는 상태
* 일반적으로 죽이거나 재부팅하면 없어짐

### 고아 프로세스(Orphan Process)

자식 프로세스보다 부모 프로세스가 먼저 죽은 경우의 프로세스

* 자식 프로세스보다 부모 프로세스가 먼저 죽었을 경우 자식 프로세스가 pid 0인 init(systemd) 프로세스에 속하게 된 경우
* 고아 프로세스가 작업을 종료하면 init 프로세스가 wait 함수를 호출하여 고아 프로세스의 종료 상태를 회수함으로써 좀비 프로세스가 되는 것을 방지함

### 명령어

* kill: 현재 실행중인 프로세스를 종료하는 명령어
  * kill -9 프로세스 번호
* jobs: 백그라운드에서 수행 중인 프로세스를 보여주는 명령어
* fg: 백그라운드에서 수행 중인 프로세스를 포어 그라운드 프로세스로 바꿔주는 명령어
* %: 백그라운드로 프로세스를 수행하게 하는 명령어
* uname: 시스템 관련 정보를 보여주는 명령어
  * uname -a: 모든 정보 확인
  * uname -s: 커널 이름 확인
* free: 메모리 관련 정보를 보여주는 명령어
  * free -m: 메가 바이트 단위로 출력
* top: 실시간으로 CPU와 메모리 사용률을 보여주는 명령어
* last: 최근 시스템을 사용한 사용자 정보를 보여주는 명령어
* 