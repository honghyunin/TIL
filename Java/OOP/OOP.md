## 객체지향

> 해당 글은 김영한님의 스프링 핵심 원리 기본편에 나오는 "객체 지향 설계와 스프링"의 내용이며 조심스레 객체지향에 대한 제 생각을 조금 곁들여 정리한 글입니다.

## 객체 지향 특징

### 추상화

> 추상화는 복잡한 자료, 모듈, 시스템 등으로부터 핵심적인 개념 또는 기능을 간추려 낸 것을 말합니다.

운전자가 자동차를 운전할 때 자동차의 내부 구조를 다 알지 못해도 운전하는 방법만 알아도 차를 앞으로 나아가게 할 수 있듯이 우리 또한 내부 구현 코드를 다 알지 못해도 추상화를 통해 이 객체가 어떤 일을 할 수 있는 지 알 수 있습니다.

### 캡슐화

> 객체의 속성(data fields)과 행위(methods)를 하나로 묶고, 실제 구현 내용 일부를 외부에 감추어 은닉합니다.

_여기서 은닉화는 캡슐화를 통해 __외부에서 객체에 접근하여 값을 변경할 수 없도록 숨기는__ 캡슐화의 __효과__ 입니다._

- 상속
> 상속은 객체들 간의 관계를 구축하여 기능을 개선하고 추가하는 방법입니다.

상속은 부모 클래스의 유산(필드, 메소드)들을 자식 클래스가 모두 이어받고, 자식 클래스에서도 부모 클래스가 가진 것들을 그대로 사용할 수도 있습니다. 또한 이 유산을 통해 새로운 것들을 추가하여 아예 다른 결과를 창출해낼 수도 있습니다.

- **다형성**

> 그 프로그래밍 언어의 자료형 체계의 성질을 나타내는 것으로, 프로그램 언어의 각 요소들(상수, 변수, 식, 오브젝트, 함수, 메소드 등)이 다양한 자료형(type)에 속하는 것이 허가되는 성질을 가리킨다. 반댓말은 단형성으로, 프로그램 언어의 각 요소가 한가지 형태만 가지는 성질을 가리킵니다.

## 객체 지향 프로그래밍

- 객체 지향 프로그래밍은 일반 프로그래밍을 컴퓨터에게 내리는 명령으로 보는 시각에서 벗어나, 여러 개의 사물과 개념이 독립된 단위인 “**객체**”가 각각의 **객체**끼리 **메시지**를 주고받으며 데이터를 처리(**협력**)하도록 개발하는 것을 의미합니다.
- 객체 지향 프로그래밍은 프로그램을 **유연**하고 **변경**이 **용이**하게 만들기 때문에 대규모 소프트웨어 개발에 많이 사용된다.

## 유연하고, 변경이 용이?

- 레고 블럭 조합하듯이
- 키보드, 마우스 갈아 끼우듯이
- 컴포넌트를 쉽고 유연하게 변경하면서 개발할 수 있는 방법


## 다형성의 실세계 비유

- 실세계와 객체 지향을 1:1로 매칭X
- 그래도 실세계의 비유로 이해하기에는 좋음
- **역할**과 **구현**으로 세상을 구분

![Untitled](/images/oop_%EB%8B%A4%ED%98%95%EC%84%B12.png)

운전자의 역할은 변하지 않고 (운전을 한다는 역할)

자동차의 역할(운전자를 태우고 운전한다)

자동차의 구현체를 바꿔도 운전자의 역할은 변하지 않음

이 뜻은

`클라이언트에게 역량을 주지않고 새로운 기능을 제공할 수 있다.`

역할과 구분으로 세상을 구분했기 때문에 이 것이 가능하다.

자동차가 새로 나와도 클라이언트(운전자)는 새로운 것을 배우지 않아도 된다.

다시말해,

운전자는 운전을 할 수만 있다면

얼마든지 자동차가 바뀌어도 운전을 할 수 있다.

다른 예를 들어보자

![Untitled](/images/oop_%EB%8B%A4%ED%98%95%EC%84%B1.png)

로미오 역할을 장동건이나 원빈이 할 수도 있고, 나나 무명 배우가 해도 로미오 역할은 수행가능하다

(줄리엣도 마찬가지로)

역할을 누가 수행하건 어쨋든 로미오 역할은 존재하고 공연은 할 수 있어야한다

이 것이 `유연하고 변경에 용이`이다.

관객은 로미오가 누구인지가 중요한 게 아니다.

줄리엣 역할이 바뀐다고 해서 로미오에게 역량을 주지 않는다.

## 역할과 구현을 분리

- **역할**과 **구현**으로 구분하면 세상이 **단순**해지고, **유연**해지며 **변경**도 편리해진다.

### 장점

- **클라이언트**는 대상의 역할(인터페이스)만 알면 된다.
- **클라이언트**는 구현 대상의 **내부 구조를 몰라도 된다**.
- **클라이언트**는 구현 대상의 **내부 구조가 변경**되어도 영향을 받지 않는다.
- **클라이언트**는 구현 **대상 자체를 변경**해도 영향을 받지 않는다.

### 자바 언어

- 자바 언어의 다형성을 활용
    - 역할 = 인터페이스
    - 구현 = 인터페이스를 구현한 클래스, 구현 객체
- 객체를 설계할 때 **역할**과 **구현**을 명확히 분리
- 객체 설계시 역할(인터페이스)을 먼저 부여하고, 그 역할을 수행하는 구현 객체 만들기

## 객체의 협력이라는 관계부터 생각

- 혼자 있는 객체는 없다.
- 클라이언트: **요청**, 서버: **응답**
- 수 많은 객체 클라이언트와 객체 서버는 서로 협력 관계를 가진다.

## 자바 언어의 다형성

- 오버라이딩을 떠올려보자
- 오버라이딩은 자바 기본 문법
- 오버라이딩 된 메서드가 실행
- 다형성으로 인터페이스를 구현한 객체를 실행 시점에 유연하게 변경할 수 있다.
- 물론 클래스 상속 관계도 다형성, 오버라이딩 적용 가능

![](/images/%EB%8B%A4%ED%98%95%EC%84%B1_2.png)

실제로 실행되는 save는 MemberService에서 save를 호출할 때 들어가있는 객체에 따라 다르다. MemoryMemberRepository라면 빨간색이 실행될 것이고, JdbcMemberRepository라면 초록색이 실행될 것이다.

![Untitled](/images/%EB%8B%A4%ED%98%95%EC%84%B1_1.png)

 부모 클래스는 모든 자식 클래스를 대입할 수 있다.

하지만 반대의 경우는 성사되지 않는다.

## 다형성의 본질

- 인터페이스를 구현한 객체 인스턴스를 **실행 시점**에 **유연**하게 **변경**할 수 있다.
- 다형성의 본질을 이해하려면 **협력**이라는 객체사이의 관계에서 시작해야함
- **클라이언트를 변경하지 않고, 서버의 구현 기능을 유연하게 변경할 수 있다.**

## 정리

- 실세계의 역할과 구현이라는 편리한 컨셉을 다형성을 통해 객체 세상으로 가져올 수 있음
- 유연하고, 변경이 용이
- 확장 가능한 설계
- 클라이언트에 영향을 주지 않는 기능
- 인터페이스를 안정적으로 잘 설계하는 것이 중요

## 한계

- 역할(인터페이스) 자체가 변하면, 클라이언트, 서버 모두에 큰 변경이 발생한다.
- 자동차를 비행기로 변경해야 한다면?
- 대본 자체가 변경된다면?
- 인터페이스를 안정적으로 잘 설계하는 것이 중요

# 스프링과 객체 지향

- 다형성이 가장 중요하다!
- 스프링은 다형성을 극대화해서 이용할 수 있게 도와준다.
- 스프링에서 이야기하는 제어의 역전(IoC), 의존관계 주입(DI)은 다형성을 활용해서 역할과 구현을 편리하게 다룰 수 있도록 지원한다.
- 스프링을 사용하면 마치 레고 블럭 조합하듯이! 공연 무대의 배우를 선택하듯이! 구현을 편리하게 변경할 수 있다.