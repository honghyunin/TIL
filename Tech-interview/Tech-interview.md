# 기술면접 준비

## Primitive Type & Wrapper Class

### Primitive Type 이란?

Primitive Type은 일반적으로 Type을 선언 해줄 때
사용하는 기본적인 타입을 의미합니다
예를 들어  `short, int, long, float, double, byte, char, boolean`와 같은 타입들이 있습니다.

### Wrapper Class

Wrapper class 는 타입이 객체안에 담겨있는 __클래스__ 입니다.

List를 사용할 때 `List<int>`로 선언하지 않습니다. 올바르지 않은 선언일 뿐더러 자바에서 기본형 타입의 List를 만드는 것은 매우 복잡한 일이기 때문입니다.

따라서 이 기본적인 타입을 객체로 감싸서 사용하는 것이 Wrapper Class입니다.

사용하기에는 용이하지만, Wrapper Class는 객체이다보니 생성하는 과정에 있어 비용이 들기 때문에 기본형을 대신해서 사용하진 않습니다.

<hr>

### 추상화
- 추상화는 복잡한 자료, 모듈, 시스템 등으로부터 핵심적인 개념 또는 기능을 간추려 낸 것을 말합니다.

### 캡슐화
> 객체의 속성(data fields)과 행위(methods)를 하나로 묶고, 실제 구현 내용 일부를 외부에 감추어 은닉합니다.

- 은닉화는 캡슐화를 통해 __외부에서 객체에 접근하여 값을 변경할 수 없도록 숨기는 것__ 입니다.

### 상속
- 상속은 객체들 간의 관계를 구축하여 기능을 개선하고 추가하는 방법입니다.

### 다형성
- 하나의 객체가 여러 형태를 이루어 다양한 기능을 구현할 수 있는 것입니다.

### 객체 지향 프로그래밍이란 무엇인가요?

- 컴퓨터 프로그래밍 패러다임 중 하나로, __프로그래밍에서 필요한 데이터를 추상화시켜 상태와 행위를 가진 객체를 만들고 그 객체들 간의 유기적인 상호작용을 통해 로직을 구성하는 프로그래밍 방법__ 입니다.

## 클래스(Class), 객체 (Object), 인스턴스 (Instance)
- 클래스는 객체의 설계도로 field(특징)와 method(행동)으로 이루어져 있습니다.

### 객체와 인스턴스
- 객체는 현실 세계의 물체나 개념 등을 속성화 시킨 것을 말합니다.
- 인스턴스는 설계도에 명시된 객체를 실제로 구현한 것입니다.

## Blocking/NonBlocking

Blocking : 함수를 호출했을 때, 작업이 완료되고 결과를 반환 받을 때까지 대기

NonBlocking : 함수를 호출했을 때, 작업이 실행되고 제어권을 호출한 함수에게 넘김

## Synchronous/Asynchronous

Synchronous : 호출된 함수의 수행 결과 및 종료를 호출한(호출된 함수뿐 아니라 호출한 함수도 함께) 함수가 신경씀

Asynchronous : 호출된 함수의 수행 결과 및 종료를 호출된 함수 혼자 직접 신경쓰고 직접 처리함
비동기

## Spring은 무엇인가요?

Spring은 Java 기반 오픈소스 애플리케이션 프레임워크입니다.
- 애플리케이션 프레임워크란 특정 기술에 국한되지 않고 애플리케이션의 범용적인 프레임워크를 말합니다.

## Spring을 사용하시는 이유는 무엇인가요? 또는 선택하신 이유는 무엇인가요?

- 제가 개인적으로 OOP와 SOLID를 좋아하기 때문입니다. 물론 다른 스텍들도 이를 구현 할 수 있겠지만, 스프링이 제공해주는 IoC와 같은 기능들, 자바 자체에 내장되어 있는 interface 나 다른 여타 기능들이 해당 개념들을 구현하기 쉽게 해주고, 또한 앞선 개념들을 지켰을 때의 프로그래밍 적으로 더 질 좋은 제품을 만들 수 있겠다고 생각이 들어 저는 스프링을 사용합니다. 

## AOP란 무엇인가요?

- AOP란 관점 지향 프로그래밍으로써, 애플리케이션 기능들의 코드 중에서 공통된 부분을 추출하여 재사용 할 수 있도록 만드는 것입니다.
    - ex) 어노테이션(@Transactional, @BeforEach, @AfterEach)

## Bean이란 무엇인가요?

- Spring Ioc Container가 관리하는 자바 객체입니다.

## Spring IoC Container란 무엇인가요?

- 스프링 프레임워크에는 IoC란 개념이 존재하는데요 이는 제어의 역전입니다. 제어의 역전이랑 개발자가 객체의 생명주기를 관리하는 것이 아닌, 프레임워크 단에서 객체의 생성과 소멸주기 등을 관리하는 것을 의미합니다.

## DI 의존성 주입에 대해 설명해주세요

- 의존성 주입이란 기능을 특정 대상에게 주입시킨다. 다시말해 기능을 모아놓은 클래스를 사용할 수 있도록 주입시키는 것이 의존성 주입이다.

## Garbage Collection 에 대해 설명해주세요

- 자바 Bean 객체는 IoC가 생명주기를 관리하여 객체들의 소멸까지 관리해주지만, 
개발자가 직접 생성하여 메모리를 사용하고 있는 객체들이 더 이상 참조되지 않을 때 Garbage Collection이 소멸하는 기능을 해줍니다. 

## ORM

- 객체와 테이블을 매핑해주는 것입니다.

## JPA

- 자바 진영의 ORM 인터페이스 API입니다.

## Persistence Context

- 자바 객체가 DB에 매핑되기 전에 거치는 컨텍스트입니다.