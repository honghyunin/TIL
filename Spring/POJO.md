# POJO
> POJO : '오래된 방식의 간단한 자바 오브젝트' _Java EE등의 중량 프레임워크들을 사용하게 되면서 해당 프레임워크에 종속된 '무거운' 객체를 만들게 된 것에 반발해서 사용하게 된 용어이다_

```java

public class UserDto {
	private String name;
	private String id;
	private String password;

	public String getName() {
		return name;
	}
	
	public String getId() {
		return id;
	}
	
	public String getPassword() {
		return password;
	}

	public void setName(String name) {
		this.name = name; 
	}
	
	public void set(String id) {
		this.id = id; 
	}
	
	public void setPassword(String password) {
		this.password = password;
	}
}
```

위와 같은 가장 기본적인 형태의 Java 객체를 POJO라 합니다.

좀 더 자세히 설명하면,

EJB 등에서 사용되는 Java Bean 이 아닌 Getter와 Setter로 구성된 가장 순수한 형태의 기본 클래스를 POJO라 하며,

"EJB란 자바 개발에 있어 로우 개발에 신경을 안쓰고 어플리케이션을 쉽게 만들어 준 기술이다."

EJB의 사용과 프로그램의 규모 증가로 특정 기술과 환경에 종속되어 의존하게 된 자바 코드는 가독성이 떨어져 유지보수에 어려움이 생기게 되고 또한, 특정 기술의 클래스를 상속받거나, 직접 의존하게 되어 확장성이 매우 떨어지며 점점 객체 지향성을 잃어갔다.

그래서 개발자들은 옛날 순수한 객체 지향성이 없던 시절로 돌아가자는 취지로 POJO를 개발하게 되었다.

이로 인해 POJO는 EJB에 비해 훌륭한 객체 단위가 될 수 있었다.

# POJO의 조건

**1. 특정 규약에 종속되지 않는다.**
- 자바 언어와 꼭 필요한 API 외에는 종속되지 않아야 한다
**2. 특정 환경에 종속되지 않는다.**
- 특정 환경에 종속되어 동작하지 않아야 한다
**3. 객체 지향적 원리에 충실해야 한다.**

# POJO 프레임워크

> POJO 프레임워크 : POJO의 장점과 EJB에서 제공하는 엔터프라이즈 서비스와 기술을 그대로 사용할 수 있도록 도와주는 프레임워크(스프링, 하이버네이트)

## 하이버네이트
> 하이버네이트 : Persistence 기술과 오브젝트-관계형 DB 매핑을 순수한 POJO를 이용해 사용할 수 있게 만드는 POJO 기반 퍼시스턴스 프레임워크이다

하이버네이트가 사용하는 POJO 엔티티들은 객체 지향적인 다양한 설게와 구현이 가능하다는 점이다.

이를 가능케 하는 것이 스프링에서 정한 표준 인터페이스, JPA가 있기에 가능하다.
스프링 개발자들은 ORM 이라는 기술을 사용하기 위해서 JPA라는 표준 인터페이스를 정해두고, 여러 ORM 프레임워크들은 이 JPA라는 표준 인터페이스 아래에서 구현되어 실행된다.
이 것이 바로 스프링이 새로운 엔터프라이즈 기술을 도입하면서도 POJO를 유지하는 방법이다.

이런 방법을 스프링의 PSA라고 이야기 한다.

## POJO 장점

- 깔끔한 코드
- 간편한 테스트
- 객체지향적인 설계를 자유롭게 적용
	- 객체지향 프로그램은 엔터프라이즈 시스템에서와 같이 복잡한 도메인을 가진 곳에서 가장 효과적으로 사용될 수 있다.

## Refrence

- [[Spring] POJO(Plain Old Java Object)란?](https://dev-coco.tistory.com/82)
- [POJO(plain old java object)란?](https://happyer16.tistory.com/entry/POJOplain-old-java-object%EB%9E%80)
- [[Spring] 스프링의 특징 - POJO란 무엇인가 :: Willing to Venture💻가보지 않은 길을 두려워하지 않습니다](https://create-something-from-nothing.tistory.com/55)