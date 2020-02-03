---
title: "JAVA 클래스의 개념과 작성"
date: 2019-08-08 12:30:00 +0900
tags:
    - Java
categories:
    - Java
---
JAVA에서 클래스는 아주 중요한 개념이다.
```java
public class Animal {
}
```
위 Animal 클래스는 가장 간단한 형태의 클래스이다. 클래스의 선언만 있고 내용은 없는 빈 껍데기이다.

하지만 이 껍데기 뿐인 클래스도 아주 중요한 기능을 가지고 있다. 그 기능은 바로 객체(Object)를 생성하는 기능이다.
```java
Animal dog = new Animal();
```
new는 객체를 생성할 때 사용하는 키워드이다. 이렇게 하면 Animal 클래스의 인스턴스(Instance)인, dog, 즉 Animal의 객체가 만들어진다.

dog는 객체이다.
dog 객체는 Animal의 인스턴스이다.즉, 인스턴스라는 말은 특정 객체가 어떤 클래스에 속하고 있다는 의미로 쓸 때 쓰인다.

위에서 만든 Animal 클래스는 껍데기만 있을 뿐이다. 이제 이를 채워 보겠다.

```java
public class Animal {
	String name;
	public void setName(String name){
		this.name = name;
	}
	public String getName(){
		return this.name;
	}
}
```
처음 작성한 Animal 클래스에 추가적으로 String 타입의 name이라는 변수를 선언하고 이를 수정하고 가져오는 메소드(setName, getName)를 작성하였다.
 이렇게 작성된 메소드는 Animal의 인스턴스에 도트연산자(.)를 사용함으로서 호출할 수 있다.

```java
Animal dog = new Animal();
dog.setName("백구");
System.out.println(dog.getName());
```

# CAUCION
이 문서는 현재 작성중인 문서입니다.
