---
title: "[자율 공부방] 학습(작업) 내용 공유 - 01"
toc: false
tags: [영남이공대학교, 자율 공부방]
categories:
  - Daily
  - SelfStudy
date: 2020-09-04 23:00:00
thumbnail: /images/post_include/daily_self-study/title.gif
---
> 영남이공대학교 자율 공부 모임에 공유할 목적으로 작성하는 포스트입니다.  
> 학습 내용에 대한 구체적인 사항은 별도 포스트에서 다룰 예정입니다.
> 개인적으로 학습하며 기록하고 있기 때문에 <font color='red'>잘못된 내용</font>이 있을 수 있습니다. 잘못된 내용이 있다면 댓글로 알려주세요.  

# JPA
## 프록시
> Member를 조회할 때 Team도 함께 조회해야 할까?
    
```java
Member findMember = em.find(Member.class, 1L);
    
// case 1
printMember(findMember);
// case 2 : findMember.getTeam()
printMemberAndTeam(findMember);
```
### EntityManager->getReference()
#### 개요
* 실제 클래스를 상속 받아서 만들어짐
* 실제 클래스와 겉 모양이 같다
* 사용하는 입장에서는 진짜 객체인지 프록시 객체인지 구분하지 않고 사용하면 됨(이론상)
* 프록시 객체는 실제 객체의 참조(target)을 보관
* 프록시 객체를 호출하면 프록시 객체는 실제 객체의 메소드 호출
```java
Member member = em.getReference(Member.class, 1L);
member.getName();
```
![](/images/post_include/daily_self-study/20200904-01.png)

#### 특징
* 프록시 객체는 처음 사용할 때 한 번만 초기화
* 프록시 객체를 초기화할 때, 프록시 객체가 실제 엔티티로 바뀌는 것은 아님. 초기화되면 프록시 객체를 통해서 실제 엔티티에 접근 가능
* 프록시 객체는 원본 엔티티를 상속 받음. 따라서 타입 체크시 주의해야함(== 비교 실패, 대신 instance of 사용)
* 영속성 컨텍스트에 찾는 엔티티가 이미 있으면 em.getReference()로 호출해도 실제 엔티티 반환(그 반대도 마찬가지)
* 영속성 컨텍스트의 도움을 받을 수 없는 준영속 상태일 때, 프록시를 초기화하면 문제 발생
    > Hibernate는 `org.hibernate.LazyInitialiizationException` 예외 발생

### 프록시 확인
* 프록시 인스턴스의 초기화 여부 확인
    `PersistenceUnitUtil->isLoaded(Object entity)`
* 프록시 클래스 확인 방법
    `entity.getClass().getName()` 출력 => `..javasist.. or ..HibernateProxy..`
* 프록시 강제 초기화
    `org.hibernate.Hibernate.initialize(entity)`
* 참고: JPA 표준은 강제 초기화가 없음.
    > 강제 호출: `member.getName()`

## 즉시 로딩과 지연 로딩
> Member를 조회할 때 Team도 함께 조회해야 할까?
```java
Team team = new Team();
team.setName("teamA");
em.persist(team);

Member member = new Member();
member.setUsername("hello");
member.setTeam(team);
em.persist(member);

em.flush();
em.clear();

Member findMember = em.find(Member.class, member.getId());

System.out.println("m = " + findMember.getTeam().getClass());
```
### 지연 로딩(LAZY)
```sql
Hibernate: 
    select
        member0_.MEMBER_ID as member_i1_3_0_,
        member0_.createdBy as createdb2_3_0_,
        member0_.createdDate as createdd3_3_0_,
        member0_.lastModifiedBy as lastmodi4_3_0_,
        member0_.lastModifiedDate as lastmodi5_3_0_,
        member0_.TEAM_ID as team_id7_3_0_,
        member0_.USERNAME as username6_3_0_ 
    from
        Member member0_ 
    where
        member0_.MEMBER_ID=?
m = class Team$HibernateProxy$vijt0TeG
```
Member만 SELECT하고 Team은 Proxy로 가져오는 모습 
### 즉시 로딩(EAGER)
```sql
Hibernate: 
    select
        member0_.MEMBER_ID as member_i1_3_0_,
        member0_.createdBy as createdb2_3_0_,
        member0_.createdDate as createdd3_3_0_,
        member0_.lastModifiedBy as lastmodi4_3_0_,
        member0_.lastModifiedDate as lastmodi5_3_0_,
        member0_.TEAM_ID as team_id7_3_0_,
        member0_.USERNAME as username6_3_0_,
        team1_.TAEM_ID as taem_id1_5_1_,
        team1_.createdBy as createdb2_5_1_,
        team1_.createdDate as createdd3_5_1_,
        team1_.lastModifiedBy as lastmodi4_5_1_,
        team1_.lastModifiedDate as lastmodi5_5_1_,
        team1_.name as name6_5_1_ 
    from
        Member member0_ 
    left outer join
        Team team1_ 
            on member0_.TEAM_ID=team1_.TAEM_ID 
    where
        member0_.MEMBER_ID=?
m = class Team
```
Member 조회 시 JOIN으로 TEAM까지 가져오는 모습

### 프록시와 즉시로딩 주의점
* 가급적 지연 로딩만 사용(특히 실무에서)
* 즉시 로딩을 적용하면 예상하지 못한 SQL이 발생
* 즉시 로딩은 JPQL에서 N+1 문제를 일으킴
* @ManyToOne, @OneToOne은 기본이 즉시 로딩. LAZY로 변경할 것
* @OneToMany, @ManyToMany는 기본이 지연 로딩
* 만약 Team도 한번에 조회하고자 한다면 JPQL fetch 조인이나 엔티티 그래프 기능을 사용할 것

#### JPQL N+1 문제
```java
List<Member> members = em.createQuery("select m from Member m", Member.class)
                  .getResultList();
```
```sql
Hibernate: 
  /* select
      m 
  from
      Member m */ select
          member0_.MEMBER_ID as member_i1_3_,
          member0_.createdBy as createdb2_3_,
          member0_.createdDate as createdd3_3_,
          member0_.lastModifiedBy as lastmodi4_3_,
          member0_.lastModifiedDate as lastmodi5_3_,
          member0_.TEAM_ID as team_id7_3_,
          member0_.USERNAME as username6_3_ 
      from
          Member member0_
Hibernate: 
  select
      team0_.TAEM_ID as taem_id1_5_0_,
      team0_.createdBy as createdb2_5_0_,
      team0_.createdDate as createdd3_5_0_,
      team0_.lastModifiedBy as lastmodi4_5_0_,
      team0_.lastModifiedDate as lastmodi5_5_0_,
      team0_.name as name6_5_0_ 
  from
      Team team0_ 
  where
        team0_.TAEM_ID=?  
```
SELECT 쿼리가 2번 나가는 모습.  
`Why?` JPQL로 Member를 조회했지만 EAGER이기 때문에 연관된 엔티티를 모두 조회. 이때 Member가 서로 다른 Team를 가질 경우 그에 해당하는 SELECT 쿼리가 추가로 실행된다. 
  
## 영속성 전이(CASCADE)
* 특정 엔티티를 영속 상태로 만들 때 연관된 엔티티도 함께 영속 상태로 만들고 싶을 때 사용
  > 예: 부모 엔티티를 저장할 때 자식 엔티티도 함께 저장
* 참조하는 곳이 하나일 때 사용!
* 특정 엔티티가 개인 소유할 때 사용!

## 고아 객체
* 정의: 구모 엔티티와 연관관계가 끊어진 자식 엔티티
* 고아 객체 제거: 이러한 고아 객체를 자동으로 삭제하게끔 지원 `orphanRemoval = true`
```java
Parent findParent = em.find(Parent.class, parent.getId());
findParent.getChildren().remove(0);
```
```sql
Hibernate: 
    /* delete domain.Child */ delete 
        from
            Child 
        where
            CHILD_ID=?
```
DELETE SQL이 실행되는 모습

### 주의 사항
* 참조가 제거된 엔티티는 다른 곳에서 참조하지 않는 고아 객체로 보고 삭제하는 기능
* 참조하는 곳이 하나일 때 사용!
* 특정 엔티티가 개인 소유할 때 사용!
* 참고: 개념적으로 부모를 제거하면 자식은 고아가 된다. 따라서 고아 객체 제거 기능을 활성화 하면, 부모를 제거할 때 자식도 함께 제거된다. 이것은 CascadeType.REMOVE처럼 작동한다.

## 영속성 전이 + 고아 객체, 생명주기
* `CasecadeType.ALL` + `orphanRemovel = true`
* 스스로 생명주기를 관리하는 엔티티는 em.persist()로 영속화, em.remove()로 제거
* 두 옵션을 모두 활성화 하면 부모 엔티티를 통해서 자식의 생명 주기를 관리할 수 잇음
* 도메인 주도 설계(DDD)의 Aggregate Root 개념을 구현할 때 유용
  > Aggregate Root 개념: 핵심이 되는 Repository를 Root로 놔두고, 그 아래 Domain은 Root에서 관리하는 개념  
