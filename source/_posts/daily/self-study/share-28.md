---
title: "[자율 공부방] 학습(작업) 내용 공유 - 28"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2021-03-21 21:30:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2021년 03월 21일 일요일
* 내용
    * 경북대학교 이용주 교수님 포스트 리딩 3건 진행했습니다.
    * Semantic Web, LOD 관련 발표 영상 2건 학습했습니다.

# 경북대학교 이용주 교수님 포스트 리딩

* https://blog.jupiterflow.com/2021/03/21/semantic_web/reading/03/
* https://blog.jupiterflow.com/2021/03/21/semantic_web/reading/04/
* https://blog.jupiterflow.com/2021/03/21/semantic_web/reading/05/

# 대용량 Linked Data 검색 서비스 현황 - 윤석찬:: 한국 시맨틱웹 콘퍼런스 (2010.12)

https://blog.jupiterflow.com/2021/03/21/semantic_web/study/01/

## Why Semantic Web failed?

* Difficult to use: 사용하기 어렵다
  * 소프트 유저, 하드 유저가 배우고 사용하기 어렵다
* No Killer application: 킬러 앱이 없다.
* Only specific domains: 특정 도메인에 집중되어 있다.
  * 의료 정보, 컨텐츠(영화, 음악) 정보 등

## Back to the Search

* RSS, Linked Data, Open API 같이 구조화된 데이터가 웹 상에 널리 퍼지기 시작함
* 일반 텍스트에서 데이터를 추출하는 것 보다 구조화된 데이터에서 데이터를 추출하는 것이 더 편리함

## Semantic Search vs Semantic Web Search

* (Semantic Search) NATE: 기존의 검색 기능에서 연관 검색어를 찾는 기능
* (Semantic Web Search) NAVER LAB: 기존의 영화 데이터베이스를 Semantic web 기반으로 표시하는 기능

## Linked Data with TBL

* Web에 Data가 돌아다닌다. 이러한 Data를 서로 Link 하는 것이 필요하다.

## LOD 검색 개발 방식

### 웹 기반 구조적 데이터 수집

* 반 구조적 데이터: HTML 내 RDFa, Microformat 혹은 HTML5
* Microdata, 구조적 데이터: XML 및 JSON, 시맨틱 데이터(RDF/RDFs)
  * 예) LDspider (GPL License)

### 데이터 저장

* Virtuoso (GPL), Sesame (BSD), Jena TDB (BSD) 혹은 RDB
* c.f Berlin SPRQL Benchmark (Nov 2009)

### 쿼리 및 데이터 분석

* SPAQL을 이용한 Query Engine

### 랭킹 및 결과 제공

* 결과에 대한 시맨틱 네비게이션 및 링크만 제공

## 기존 시맨틱 웹 처리 방법

아주 작은 도메인에서는 큰 성능 이슈 없이 처리할 수 있음.

* 모델 만들기
  * 개념과 관계 속성에 대한 정의
  * 최대한 현실에 부합하는 모델을 만들며 확장 유연성
* RDF 처리
  * 대개 기존 DB에서 변환
  * RDF, Triple, N-Triple 형태 저장
  * 처리 시간이 길다
* SPARQL 질의
  * 원하는 답을 얻기 위한 추론
  * 응답 시간이 길다

## 검색에서 클라우드 플랫폼의 장점

* 사회적 이슈가 발생했을 때, 클라우드 동적 제어 API를 이용하여 크롤링 및 인덱싱 작업을 비주기적으로 시행
* UCC 검색 콘텐츠 DB에 대해서 신규 작업 시 클라우드 기반으로 테스트 가능
* Hadoop, Hbase 등 각종 분산 컴퓨팅 자원을 필요 시 이용
* 실시간 웹(Realtime Web) 검색을 대응하기 위한 검색 엔진 및 처리 시스템 필요

## 클라우드 기반 LOD 검색 방식

* 웹 기반 구조적 데이터 수집
* 데이터 처리
  * Hadoop을 이용한 분산 컴퓨팅 플랫폼
  * 대용량 RDF 변환 및 처리
  * NoSQL을 이용한 검색 데이터 저장소
* 쿼리 및 데이터 분석
  * 사용자 쿼리에 해당하는 질의어 분석
  * 질의어를 통한 SPARQL 쿼리 생성
  * 쿼리에 대한 서브 쿼리 자동 생성 및 AnwserSet 추출
* 랭킹 및 결과 제공
  * 관계 기반 질의어 확장 및 추천

### Key Value DB for heavy update

Update Heavy job, Real-time incremental Update

# 시맨틱 웹 소개 (Semantic Web)

https://blog.jupiterflow.com/2021/03/21/semantic_web/study/02/

## 시맨틱 웹이란?

### 일반 웹과 시맨틱 웹

* 일반 웹: 정보의 의미를 컴퓨터가 알지 못함
* 시맨틱 웹: 정보의 의미를 컴퓨터가 알 수 있게 함
  현재의 인터넷에서 리소스에 대한 정보와 자원 사이의 관계를 온톨로지 형태로 표현해서, 기계가 처리하도록 하는 프레임워크이자 기술

### 강한 시맨틱 기술

* 의미, 메타데이터 자동생성(RDF, RDFa, 등의 활용)
* 대용량 지식 베이스의 구축과 질의
* 온톨로지 및 규칙 기반 질의와 추론
* 상황인지 등과 연계 가능한 검색 서비스

### 약한 시맨틱 기술

* 키워드 및 개체명을 중심으로 한 특성 추출
* 정보의 구조화 통계에 기반한 의미 분석
* 공기어 분석, LSA (Latent Semantic Analysis) 등의 기법이 활용됨
* 정보의 군집과 분석
* 자동 분류와 요약

## 온톨로지란?

* 아리스토텔레스가 최초로 사용한 개념
  * 해->뜨겁다 / 밝다 / 낮 / 떠오르다 / 아침 / 둥근 / 하늘 /. ..
* 정보를 기계가 처리할 수 있는 형태로 표현
* 정보들의 관계를 정의하는 사전

### 온톨로지 사례

* 남자<->여자 : 결혼이라는 관계를 정의하면 '부부'라는 의미가 명확해짐

## DB vs KB

### 기존의 Table DB 구조

* PK를 중심으로 엮어내는 형태
* 변경사항이 생기면 점점 복잡해짐
* 변화대응이 러엽고 관계정의가 어렵다

### Knowledge Base 구조

* S, V, O 구조
  * S(주어): Apple Tree, Apple Tree, Apple Tree, Apple Tree
  * V(동사): 이다, 영업시작한다, 이다, 주점으로 변한다
  * O(목적어): 식당, 10AM, 주점, 10PM
* 데아터구조 변화에 자유롭다
* 개념간의 관계정의 및 편집이 자유롭다

### 검색의 차이

* 기존의 Table DB 검색: SQL을 이용해 DB Table에 질의를 하는 방식. DB에 있는 정보만 보여줌
  * Closed Search
  * 내부 DB의 정보만 단순 검색
* Knowledge Base 검색: SPARQL을 연결된 모든 URI에 질의를 보냄. 연관된 정보를 함께 보여주는 시맨틱 검색 가능
  * Open Search
  * 연결된 모든 정보를 가져오는 연관검색

## 시맨틱웹 적용

### 일반웹을 시맨틱으로 바꾸려면?

* 온톨로지 설계: DB -> KB
* KB 구축 자동화
  * 데이터 자동 수집
  * 데이터 필터링
  * 조건・규제 구문 추출
  * 관리자 확인・편집
  * KB 생성
* 시맨틱 검색