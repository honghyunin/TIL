
# JPA

- EJB
    - 과거의 자바 표준(Entity Bean)
    - 과거의 ORM
    - 문제
        - 코드가 매우 지저분하다.
        - API의 복잡성이 높다. (많은 interface 구현)
        - 속도가 느리다
- Hiberante
    - ORM 프레임워크, Open Source SW
    - 'Gaving King'과 시러스 테크놀로지스 출신 동료들이 EJB2 스타일의 Entity Beans 이용을 대체할 목적으로 개발하였다.
- JPA (Java Persistence API)
    - 현재 자바 ORM 기술 표준으로, ``인터페이스 모음``이다.
        - 즉, 실제로 JPA만 가지고는 동작하지 않는다.
        - JPA 인터페이스를 구현한 대표적인 오픈소스가 Hibernate이다.

# JPA 동작 과정

![JPA 동작과정 1](img/JPA_동작과정1.png)

- JPA는 애플리케이션과 JDBC 사이에서 동작한다.
    - 개발자가 JPA를 사용하면, JPA 내부에서 JDBC API를 사용하여 SQL을 호출해 DB와 통신한다.
    - 즉, 개발자가 직접 JDBC API를 쓰는 것이 아니다.

## 저장 과정

![JPA 동작과정 1](img/JPA_저장과정.png)

- MemberDAO에서 객체를 저장하고 싶을 때
    - 개발자는 JPA에 Member 객체를 넘긴다.
    - JPA는
        - 1) Member 엔티티를 분석한다.
        - 2) INSERT SQL을 생성한다
        - 3) JDBC API를 사용하여 SQL을 DB에 날린다.
- 쿼리를 JPA가 만들어주기 때문에 Object와 RDB간의 **패러다임 불일치를 해결**할 수 있다.

# 🙆‍♂️ 참고 🙇‍♂️

- __[[ JPA란 ](https://gmlwjd9405.github.io/2019/08/04/what-is-jpa.html)]__



- __[[ JPA란 무엇인가? ](https://blog.woniper.net/255)]__