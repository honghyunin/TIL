
# JPA

- EJB
    - 과거의 자바 표준(Entity Bean)
    - 과거의 ORM
    - 문제
        - 코드가 매우 지저분합니다.
        - API의 복잡성이 높습니다. (많은 interface 구현)
        - 속도가 느립니다
- Hiberante
    - ORM 프레임워크, Open Source SW
    - 'Gaving King'과 시러스 테크놀로지스 출신 동료들이 EJB2 스타일의 Entity Beans 이용을 대체할 목적으로 개발하였습니다.
- JPA (Java Persistence API)
    - 현재 자바 ORM 기술 표준으로, `인터페이스 모음` 입니다.
        - 즉, 실제로 JPA만 가지고는 동작하지 않습니다.
        - JPA 인터페이스를 구현한 대표적인 오픈소스 : Hibernate

# JPA 동작 과정

![JPA 동작과정 1](img/JPA_동작과정1.png)

- JPA는 애플리케이션과 JDBC 사이에서 동작
    - 개발자가 JPA를 사용하면, JPA 내부에서 JDBC API를 사용하여 SQL을 호출해 DB와 통신
    - 즉, 개발자가 직접 JDBC API를 쓰는 것이 아닙니다.

## 저장 과정

![JPA 동작과정 1](img/JPA_저장과정.png)

- MemberDAO에서 객체를 저장하고 싶을 때
    - 개발자는 JPA에 Member 객체를 넘긴다.
    - JPA는
        - 1) Member 엔티티를 분석
        - 2) INSERT SQL을 생성
        - 3) JDBC API를 사용하여 SQL을 DB에 날린다.
- 쿼리를 JPA가 만들어주기 때문에 Object와 RDB간의 **패러다임 불일치를 해결**할 수 있습니다.

## Entity 클래스

- Entity 클래스에는 Setter 메소드를 절대 만들지 않습니다.

왜냐하면 해당 클래스의 인스턴스 값들이 언제 어디서 변해야 하는 지 코드상으로 명확하게 구분할 수가 없기 때문입니다.

## 그렇다면 어떻게 DB값을 채우나요?

기본적으론 **생성자를 통해** 최종값을 채운 후 DB에 삽입합니다.

“값 변경이 필요한 경우” **해당 이벤트에 맞는 public 메소드를 호출**하여 변경하는 것을 전제로 합니다.

 하지만 이 글에서는 생성자 대신 @Builder를 통해 제공되는 빌더 클래스를 사용합니다. 빌더는 생성자와 같은 역할을 하지만 어느 필드에 어떤 값을 채워야하는 지 명확하게 인지할 수 있습니다.

 ## Join과 Fetch Join의 차이

- 일반 조인
    - 오직 조회하는 주체가 되는 엔티티만 조회하여 영속화합니다.
    - 일반 조인은 실제 쿼리에 join이 존재하긴 하지만, join 대상에 영속성까는 관여하지 않아 값을 사용할 수 없습니다.

- 페치 조인
    - Fetch Join이 걸린 Entity를 모두 영속화하기 때문에 조회하는 주체가 되는 엔티티와 연관된 엔티티를 모두 조회하여 영속화합니다.
    - 연관된 엔티티를 모두 조회하기 때문에 즉시로딩 Entity를 참조하더라도 이미 영속화되어 영속성 컨텍스트에 있기 때문에 새로 쿼리를 날리지 않아 N + 1이 발생하지 않습니다.


# 🙆‍♂️ 참고 🙇‍♂️

- __[[ JPA란 ](https://gmlwjd9405.github.io/2019/08/04/what-is-jpa.html)]__

- __[[ JPA란 무엇인가? ](https://blog.woniper.net/255)]__

- __[[ [JPA] 일반 Join과 Fetch Join의 차이 ]](https://cobbybb.tistory.com/18)__