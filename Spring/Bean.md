# [Bean] 빈

> Bean : Spring Ioc Container가 관리하는 자바 객체, Spring Bean Container에 존재하는 객체를 말한다.

보통 개발자가 주체적으로 객체를 생성하고, 소멸하지만, 스프링에선 해당 과정을 Spring IoC Container에 의해 인스턴스화, 관리, 생성됩니다.

Bean Container는 의존성 주입을 통해 Bean 객체를 사용할 수 있도록 해줍니다.

Spring에서 **Bean은 보통 Singleton으로 존재** 합니다.

> Singleton : 클래스에서 하나의 인스턴스만을 생성하여 사용하는 것 

Spring에서 POJO(Plain Old Java Object)를 Beans 라고 부릅니다.

## POJO
> POJO : 본래 자바의 장점을 살리는 특정 '기술'에 종속되어 동작하는 것이 아닌 '오래된' 방식의 '순수한' 자바객체

> Beans는 Applicaiton의 핵심을 이루는 객체이며, 대부분 
      Container에 공급하는 설정 메타 데이터(XML 파일)에 의해 생성됩니다.
      Container는 이 메타 데이터를 통해 Bean의 생성, Bean Life Cycle, Bean Dependency(종속성)등을 알 수 있습니다.

# 어떤게 Bean일까?

우리가 생성하는 객체 new를 사용하거나 Builder 패턴을 통해 생성한 객체가 Bean이 아닌,

우리가 Spring을 통해 개발을 하다 보면 서비스 로직을 작성할 때 다른 `interface`나 `service`를 서비스 클래스에서 field로 선언하여 의존성을 주입할 때가 있다.
이때 의존성을 주입하는 클래스들은 대부분 Bean이며, 해당 클래스들은 대부분 `@Component`를 가지고 있는 `@Service`나 `@Repository`, `@Configuration` 과 같은 어노테이션을 달고 있다.


# 🙆‍♂️ 참고 🙇‍♂️

[gillog님의 게시글](https://velog.io/@gillog/Spring-Bean-%EC%A0%95%EB%A6%AC)