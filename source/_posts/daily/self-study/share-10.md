---
title: "[자율 공부방] 학습(작업) 내용 공유 - 10"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2020-09-13 22:06:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# 개요
* 날짜: 2020년 09월 13일 일요일
* 내용: JPA 학습을 했습니다. JPQL, 페이징 API, Fetch Join, 다형성 쿼리, 벌크 연산 등

# JPA
## JPQL(Java Persistence Query Language)
* JPQL은 객체지향 쿼리 언어다. 따라서 테이블을 대상으로 쿼리하는 것이 아니라 엔티티 객체를 대상으로 쿼리한다.
* JPQL은 SQL을 추상화해서 특정 데이터베이스 SQL에 의존하지 않는다.
* JPQL은 결국 SQL로 변환된다.

### 문법
* select m from Member as m where m.age > 18
* 엔티티와 속성은 대소문자 구분 O (Member, age)
* JPQL 키워드는 대소문자 구분 X (SELECT, FROM, where)
* 엔티티 이름 사용, 테이블 이름 아님(Member)
* 별칭은 필수(m), as는 생략 가능
 
### 집합과 정렬
 ```sql
select
    COUNT(m),   // 회원 수
    SUM(m.age), // 나이 합
    AVG(m.age), // 평균 나이
    MAX(m.age), // 최대 나이
    MIN(m.age)  // 최소 나이
from Member m
```
* GROUP BY, HAVING, ORDER BY 모두 동일하게 사용

### TypeQuery, Query
* TypeQuery: 반환 타입이 명확할 때 사용
* Query: 반환 타입이 명확하지 않을 때 사용

### 결과 조회 API
* query.getResultList(): 결과가 하나 이상일 때, 리스트 반환
    * 결과가 없으면 빈 리스트 반환
* query.getSingleResult(): 결과가 정확히 하나, 단일 객체 반환
    * 결과가 없으면: javax.persistence.NoResultException
    * 결과가 둘 이상이면: javax.persistence.NonUniqueResultException 
    
### 프로젝션
* SELECT 절에 조회할 대상을 지정하는 것
* 프로젝션 대상: 엔티티, 임베디드 타입, 스칼라 타입(숫자, 문자 등 기본 데이터 타입)
* DISTINCT로 중복 제거 가능

#### 엔티티 프로젝션
> 영속성 컨텍스트에서 관리
```sql
SELECT m FROM Member m
SELECT m.team FROM Member m
```

#### 임베디드 타입 프로젝션
```sql
SELECT m.address FROM Member m
```

#### 스칼라 타입 프로젝션
```sql
SELECT m.username, m.age FROM Member m
```

#### 여러 값 조회
* SELECT m.username, m.age FROM Member m
1. Query 타입으로 조회
2. Object[] 타입으로 조회
3. new 명령어로 조회
    * 단순 값을 DTO로 바로 조회
        ```sql
        SELECT new jpql.MemberDTO(m.username, m.age) FREOM Member m
        ```
    * 패키지 명을 포함한 전체 클래스 명 입력
    * 순서와 타입이 일치하는 생성자 필요
    
## 페이징 API
* JPA는 페이징을 다음 두 API로 추상화
* setFirstResult(int start Position): 조회 시작 위치(0부터 시작)
* setMaxResults(int maxResult): 조회할 데이터 수

## 조인
* 내부 조인
    ```sql
    SELECT m FROM Member m [INNER] JOIN m.team t
    ```
* 외부 조인
    ```sql
    SELECT m FROM Member m LEFT [OUTER] JOIN m.team t
    ```
* 세타 조인
    ```sql
    SELECT count(m) FROM Member m, Team t WHERE m.username
    ```

### ON 절
* ON 절을 활용한 조인(JPA 2.1부터 지원)
    1. 조인 대상 필터링
        > EX) 회원과 팀을 조인하면서, 팀 이름이 A인 팀만 조인
        
        **JPQL**
        ```sql
        SELECT m, t FROM Member m LEFT JOIN m.team t ON t.name = 'A'
        ```
        **SQL**
        ```sql
        SELECT m.*, t.* FROM
        Member m LEFT JOIN Team t ON m.TEAM_ID=t.id and t.name = 'A'
        ```
    2. 연관관계 없는 엔티티 외부 조인(하이버네이트 5.1부터) 
        > EX) 회원의 이름과 팀의 이름이 같은 대상 외부 조인
        
        **JPQL**
        ```sql
        SELECT m, t FROM
        Member m LEFT JOIN Team t ON m.username = t.name
        ```
        **SQL**
        ```sql
        SELECT m.*, t.* FROM
        Member m LEFT JOIN Team t ON m.username = t.name
        ```

## 서브 쿼리
* 나이가 평균보다 많은 회원
    ```sql
    select m from Member m
    where m.age > (select avg(m2.age) from Member m2) 
    ```
* 한 건이라도 주문한 고객
    ```sql
    select m from Member m
    where (select count(o) from Order o where m = o.member) > 0
    ```

### 지원 함수
* [NOT] EXISTS: 서브쿼리에 결과가 존재하면 참
    * {ALL | ANY | SOME}
    * ALL 모두 만족하면 참
    * ANY, SOME: 같은 의미, 조건을 하나라도 만족하면 참
* [NOT] IN: 서브쿼리의 결과 중 하나라도 같은 것이 있으면 참

### JPA 서브 쿼리 한계
* JPA는 WHERE, HAVING 절에서만 서브 쿼리 사용 가능
* SELECT 절도 가능(하이버네이트에서 지원)
* FROM 절의 서브 쿼리는 현재 JPQL에서 불가능
    * 조인으로 풀 수 있으면 풀어서 해결
    
## JPQL 타입 표현
* 문자: 'HELLO', 'She''s'
* 숫자: 10L(Long), 10D(Double), 10F(Float)
* Boolean: TRUE, FALSE
* ENUM: jpabook.MemberType.Admin (패키지명 포함)
* 엔티티 타입: TYPE(m) = Member (상속 관계에서 사용)

## 조건식 - CASE 식
* 기본 CASE 식
    ```sql
    select
        case when m.age <= 10 then '학생요금'
             when m.age >= 60 then '경로요금'
             else '일반요금'
        end
    from Member m
    ```

* 단순 CASE 식
    ```sql
    select
        case t.name
             when '팀A' then '인센티브110%'
             when '팀B' then '인센티브120%'
             else '인센티브105%'
        end
    from Team t
    ```
  
* COALESCE: 하나씩 조회해서 null이 아니면 반환
    > 사용자 이름이 없으면 이름 없는 회원을 반환
    ```sql
    select coalecse(m.username, '이름 없는 회원') from Member m
    ```
* NULLIF: 두 값이 같으면 null 반환, 다르면 첫 번째 값 반환
    > 사용자 이름이 '관리자'면 null을 반환하고 나머지는 본인의 이름을 반환
    ```sql
    select NULLIF(m.username, '관리자') from Member m
    ```

## JPQL 기본 함수
* CONCAT
* SUBSTRING
* TRIM
* LOWER, UPPER
* LENGTH
* LOCATE
* ABS, SQRT, MODE
* SIZE, INDEX(JPA 용도)

## 경로 표현식
* .(점)을 찍어 객체 그래프를 탐색하는 것
```sql
select m.username       // 상태 필드
    from Member m
        join m.team t   // 단일 값 연관 필드
        join m.orders o // 컬렉션 값 연관 필드
where t.name = '팀A'
```

### 용어 정리
* 상태 필드(state field): 단순히 값을 저장하기 위한 필드
* 연관 필드(association field): 연관관계를 위한 필드
    * 단일 값 연관 필드:
        @ManyToOne, @OneToOne, 대상이 엔티티(ex: m.team)
    * 컬렉션 값 연관 필드:
        @OneToMany, @ManyToMany, 대상이 컬렉션(ex: m.orders)

### 특징
* 상태 필드(state field): 경로 탐색의 끝, 탐색 X
* 단일 값 연관 경로: 묵시적 내부 조인(inner join) 발생, 탐색 O
* 컬렉션 값 연관 경로: 묵시적 내부 조인 발생, 탐색 X
    > FROM 절에서 명시적 조인을 통해 별칭을 얻으면 별칭을 통해 탐색 가능

### 실무 조언
* 가급적 묵시적 조인 대신 명시적 조인 사용
* 조인은 SQL 튜닝에 중요 포인트
* 묵시적 조인은 조인이 일어나는 상황을 한눈에 파악하기 어려움

## JPQL의 Fetch Join
* SQL 조인 종류 X
* JPQL에서 성능 최적화를 위해 제공하는 기능
* 연관된 엔티티나 컬렉션을 SQL 한 번에 함께 조회하는 기능
* join fetch 명령어 사용
* Fetch join ::= [ LEFT [OUTER] | INNER ] JOIN FETCH 조인경로

### Entity Fetch Join
* 회원을 조회하면서 연관된 팀도 함께 조회(SQL 한 번에)
* SQL을 보면 회원 뿐만 아니라 팀(T.*)도 함께 SELECT
* **[JPQL]**
    ```sql
    select m from Member m join fetch m.team 
    ```
* **[SQL]**
    ```sql
    SELECT M.*, T.* FROM MEMBER M 
    INNER JOIN TEAM T ON M.TEAM_ID = T.ID
    ```
  
### Collection Fetch Join
* 일대다 관계
* **[JPQL]**
    ```sql
    select t
    from Team t join fetch t.members
    where t.name = '팀A' 
    ```
* **[SQL]**
    ```sql
    SELECT T.*, M.*
    FROM TEAM T
    INNER JOIN MEMBER M ON T.ID = M.TEAM_ID
    WHERE T.NAME = '팀A'
    ```
### Fetch Join과 DISTINCT
* SQL의 DISTINCT는 중복된 결과를 제거하는 명령
* JPQL의 DISTINCT 2가지 기능 제공
    1. SQL에 DISTINCT를 추가
    2. 애플리케이션에서 엔티티 중복 제거

## Fetch Join과 일반 조인의 차이
* Fetch Join을 사용할 때만 연관된 엔티티도 함께 조회(즉시 로딩)
* Fetch Join은 객체 그래프를 SQL 한번에 조회하는 개념 

## Fetch Join의 특징과 한계
* Fetch Join 대상에는 별칭을 줄 수 없다.
    > 하이버네이트는 가능, 가급적 사용 X
* 둘 이상의 컬렉션은 Fetch Join 할 수 없다.
* 컬렉션을 Fetch Join하면 페이징 API를 사용할 수 없다.
    * 일대일, 다대일 같은 단일 값 연관 필드들은 Fetch Join 해도 페이징 가능
    * 하이버네이트는 경고 로그를 남기고 메모리에서 페이징(매우 위험)
* 연관된 엔티티들을 SQL 한 번으로 조회 - 성능 최적화
* 엔티티에 직접 적용하는 글로벌 로딩 전략보다 우선함
    * @OneToMany(fetch = fetchType.LAZY) // 글로벌 로딩 전략
* 실무에서 글로벌 로딩 전략은 모두 지연 로딩
* 최적화가 필요한 곳은 Fetch Join 적용

## Fetch Join 정리
* 모든 것을 Fetch Join으로 해결할 수는 없음
* Fetch Join은 객체 그래프를 유지할 때 사용하면 효과적
* 여러 테이블을 Join해서 엔티티가 가진 모양이 아닌 전혀 다른 결과를 내야 한다면, Fetch Join보다는 일반 Join을 사용하고 필요한 데이터들만 조회해서 DTO로 반환하는 것이 효과적

## 다형성 쿼리
### TYPE
* 조회 대상을 특정 자식으로 한정
* EX) Item 중 Book, Movie를 조회
* [JPQL]
    ```sql
    select i from Item i
    where type(i) IN (Book, Movie)
    ```
* [SQL]
    ```sql
    select i.* from Item i
    where i.DTYPE in ('Book', 'Movie')
    ```

### TREAT(JPA 2.1)
* 자바의 타입 캐스팅과 유사
* 상속 구조에서 부모 타입을 특정 자식 타입으로 다룰 때 사용
* FROM, WHERE, SELECT(하이버네이트 지원)에서 사용
* EX) 부모인 Item과 자식 Book이 있다.
* [JPQL]
    ```sql
    select i from Item i
    where treat(i as Book).author = 'kim'
    ```
* [SQL]
    ```sql
    select i.* from Item i
    where i.DTYPE = 'Book' and i.author = 'kim'
    ```  

## 엔티티 직접 사용 - 기본 키 값
* JPQL에서 엔티티를 직접 사용하려면 SQL에서 해당 엔티티의 기본 키 값을 사용
* [JPQL]
    ```sql
    select count(m.id) from Member m // 엔티티의 아이디를 사용
    select count(m) from Member m    // 엔티티를 직접 사용
    ```
* [SQL](JPQL 둘 다 아래 SQL 실행)
    ```sql
    select count(m.id) as cnt from from Member m
    ```

## Named 쿼리
* 쿼리에 이름을 부여하는 어노테이션
* 미리 정의해서 이름을 부여해두고 사용하는 JPQL
* 정적 쿼리
* 어노테이션, XML에 정의
* 애플리케이션 로딩 시점에 초기화 후 재사용
* 애플리케이션 로딩 시점에 쿼리를 검증

## 벌크 연산
* 재고가 10개 미만인 모든 상품의 가격을 10% 상승하려면?
* JPA 변경 감지 기능으로 실행하려면 너무 많은 SQL 실행
    1. 재고가 10개 미만인 상품을 리스트로 조회한다.
    2. 상품 엔티티의 가격을 10% 증가한다.
    3. 트랜잭션 커밋 시점에 변경감지가 동작한다.
* 변경된 데이터가 100건이라면 100번의 UPDATE SQL 실행

### 예제
* 쿼리 한 번으로 여러 테이블 로우 변경(엔티티)
* executeUpdate()의 결과는 영향받은 엔티티 수 반환
* UPDATE, DELETE 지원
* INSERT(insert into .. select, 하이버네이트 지원)

### 주의 사항
* 벌크 연산은 영속성 컨텍스트를 무시하고 데이터베이스에 직접 쿼리
    * 방법 1) 벌크 연산을 먼저 실행
    * 방법 2) 벌크 연산 수행 후 영속성 컨텍스트 초기화