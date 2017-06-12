---
layout: post
title: "디자인패턴 복습 및 정리"
description: 
headline: 
modified: 2017-06-12
category: designpattern
tags: [designpattern]
image: 
  feature: 
comments: true
mathjax: 
---
# Design Pattern

## SOLID Principle

### SRP(Single Resposibility Principle)

***소프트웨어의 설계 부품(클래스, 함수 등)은 단 하나의 책임만을 가져야 한다.***

* 여기서 책임이란 '기능'으로 볼 수 있다.

* 만약 한 클래스가 여러 기능을 수행한다면 해당 클래스는 책임이 많아진다. 책임이 많을 수록 클래스 내부의 함수끼리 강한 결합이 발생할 가능성이 높아진다.

### OCP(Open-Closed Principle)

***기존의 코드를 변경하지 않고(Closed) 기능을 수정하거나 추가할 수 있도록(Open) 설계해야 한다.***

* OCP를 만족하는 설계의 핵심은 **변경되는 것이 무엇인지**에 초점을 맞추는 것이다.

* 자주 변경되는 내용은 수정하기 쉽게 설계하고, 변경되지 않아야 하는 것은 수정되는 내용에 영향을 받지 않게 하는 것이 포인트다.

* OCP를 만족하기 위해 주로 사용되는 문법이 인터페이스(Interface)이다.

### LSP(Liskov Substitution Principle)

***자식 클래스는 부모 클래스에서 가능한 행위를 수행할 수 있어야 한다.***

* 리스코프 치환 원칙은 MIT Computer Science 교수인 Liskov가 제안한 설계 원칙이다.

* 부모 클래스와 자식 클래스 사이의 행위에는 일관성이 있어야 한다는 원칙이며, 이는 객체 지향 프로그래밍에서 부모 클래스의 인스턴스 대신 자식 클래스의 인스턴스를 사용해도 문제가 없어야 한다는 것을 의미한다.

* 따라서 상속 관계에서는 일반화 관계(IS-A)가 성립해야 한다.

### ISP(Interface Segregation Principle)

***클래스는 자신이 사용하지 않는 인터페이스를 구현하지 말아야 한다. 하나의 일반적인 인터페이스보다 여러 개의 구체적인 인터페이스가 낫다.***

* 자신이 사용하지 않는 기능(인터페이스)에는 영향을 받지 말아야 한다는 의미이다.

### DIP(Dependency Inversion Principle)

***의존 관계를 맺을 때, 변화하기 쉬운 것보다 변화하기 어려운 것에 의존해야한다는 원칙이다.***

* 여기서 변화하기 쉬운 것이란 구체적인 것을 뜻하고, 변화하기 어려운 것이란 추상적인 것을 뜻한다.

* 객체지향 관점에서는 변화하기 쉬운 것이란 구체화된 클래스를 의미하고, 변화하기 어려운 것은 추상 클래스나 인터페이스를 의미한다.

* DIP를 만족한다는 것은 의존 관계를 맺을 때, 구체적인 클래스보다 인터페이스나 추상 클래스와 관계를 맺는다는 것을 의미한다.

---

내용 인용 : <http://dev-momo.tistory.com/entry/SOLID-%EC%9B%90%EC%B9%99>