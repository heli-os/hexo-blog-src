---
title: "[자율 공부방] 학습(작업) 내용 공유 - 03"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2020-09-06 23:05:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2020년 09월 06일 일요일
* 내용: 주말이라 따로 공부는 안하고 새로운 프로젝트를 위해 탐색 + 설계를 조금 했습니다.

# 토이 프로젝트 - SNS 초기 설계
* URL: [http://bit.ly/2F2oPKgd](http://bit.ly/2F2oPKgd)
## Theme(candidate)
![](https://i.imgur.com/DGLvkQx.png)

## Features(by BDD)
### Member
#### Sign-up
* Parameters: display_name, email, password, password_repeat, term_agreement
* Logic
    * Client
        1. Input the parameters by user
        2. Server request
    * Server
        * When parameter validator is return 'abnormal'
            * response the 403 Forbidden error(temp)
        * When not
            * generate the salt
            * store the data to `Member(temp)`
            * response the 200 success

#### Sign-in
* Parameters: email, password
* Logic
    * Client
        1. Input the parameters by user
        2. Request to server
    * Server
        1. When parameter validator is return 'abnormal' 
            * response the 400 Bad Request
        2. When not
            * Validate the Member(from client) with `Member(temp)`
            * When validate result is 'abnormal'
                * response the 403 Forbidden error(temp)
            * When not
                * generate the session(?)
                * something more....
                * response the 200 success
#### Find-member
...

### Feed
#### Post-new-feed
* Parameters: description, media(photo/video)
* Logic
    * Client
        1. Input the parameters by user
        2. Request to server
    * Server
        1. When parameter validator is return 'abnormal' 
            * response the 400 Bad Request
        2. When not
            * Authorize the request using Authorization Header
            * When Authorize result is 'abnormal'
                * response the 403 Forbidden error
            * When not
                * store the data to `Feed(temp)`
                * response the 200 success


something more...