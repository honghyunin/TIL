# [Bean] 빈

| ``Bean`` : ``Spring Ioc Container``가 관리하는 자바 객체, ``Spring Bean Container``에 존재하는 객체를 말한다.

``Spring IoC(Inversion of Control) Container``에 의해 인스턴스화, 관리, 생성됩니다.

``Bean Container``는 의존성 주입을 통해 Bean 객체를 사용할 수 있도록 해줍니다.

Spring에서 **``Bean``은 보통 ``Singleton``으로 존재** 합니다.

- Singleton : 어떤 Class가 최초 한 번만 메모리를 할당하고(Static) 그 메모리에 객체를 만들어 사용하는 디자인 패턴

**Spring에서** ``POJO(Plain Old Java Object)``를 ``Beans`` 라고 부릅니다.

## POJO
| POJO : 본래 자바의 장점을 살리는 특정 '기술'에 종속되어 동작하는 것이 아닌 '오래된' 방식의 '순수한' 자바객체

> ``Beans``는 Applicaiton의 핵심을 이루는 객체이며, 대부분 
      ``Container``에 공급하는 설정 메타 데이터(XML 파일)에 의해 생성됩니다.
      ``Container``는 이 메타 데이터를 통해 ``Bean``의 생성, ``Bean Life Cycle``, ``Bean Dependency(종속성)``등을 알 수 있습니다.

new 연산자로 생성하는 객체는 ``Bean``이 아니고, ``AplicationContext.getBean()``으로 얻어질 수 있는 객체는``Bean``입니다.

즉, Spring에서의 Bean은 Applicationtext가 알고있는 객체, 즉 AplicationContext가 만들어서 그 안에 담고있는 객체를 의미합니다.

# 어떤게 Bean일까?

- 우리가 new 연산자로 어떤 객체를 생성했을 때 (X)
- ApplicationContext.getBean()으로 얻어진 객체(O)

즉 Spring에서의 빈은 ApplicationContext가 만들어서 그 안에 담고있는 객체를 의미합니다.


# 🙆‍♂️ 참고 🙇‍♂️

[gillog님의 게시글](https://velog.io/@gillog/Spring-Bean-%EC%A0%95%EB%A6%AC)
