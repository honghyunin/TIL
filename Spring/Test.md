# 단위 테스트 - Unit Test
> 단위 테스트 : 응용 프로그램에서 테스트 가능한 가장 작은 소프트웨어를 실행하여 예상대로 동작하는지 확인하는 테스트

- **개발자 관점**
- 단위 테스트의 대상의 범위는 엄격하게 정해져 있지만, 일반적으로 클래스, 메소드 수준으로 정해진다.
- 대상의 크기에 따라 다르지만, 작을 수록 복잡성이 낮아지며 동작을 표현하기 쉬워진다.

**정리**
- 단위 테스트 대상의 범위를 작게 설정해서 단위 테스트를 최대한 간단하고 디버깅하기 쉽게 작성해야 한다.

프로그래밍 언어마다 단위 테스트에서 사용하는 프레임워크가 다르다.
Java는 주로 `Junit`으로 아래와 같이 테스트한다.

```java
@DisplayName("기상한다")
@Test
public void wakeUp() {
	//given
	User user = new User("hyunin");

	//when
	user.wakeUp();

	//then
	assertThat(user.isStatus()).isEqualtTo(1);
}
```

# 통합 테스트 - Integration Test
> 통합 테스트 : 큰 동작을 달성하기 위해 여러 모듈들을 모아 이들이 의도대로 협력하는 지 확인하는 테스트

- **개발자 관점**
- 통합 테스트는 작은 단위의 테스트들을 묶어 검증하거나, DB, 다양한 환경에서 수행하는 것이다
- 단위 테스트에서 찾지 못하는 연동 시 발생하는 버그를 찾을 수 있다

스프링부트에는 `@SpringBootTest` 어노테이션을 통해 통합 테스트를 진행할 수 있다

```java
@SpringBootTest
class HongsinsaApplicationTests {
    @Test
    void contextLoads() {
    }
}
```


# 인수 테스트 - Acceptance Test

> 인수 테스트 : 사용자의 입장에서 시나리오에 맞춰 수행하는 테스트

- **사용자 관점의 테스트**
- 비즈니스 쪽에 초점을 두며, 프로젝트에 참여하는 사람들이 토의해서 시나리오를 만들고, 개발자를 이에 따라 코드를 작성한다.
	- 개발자가 직접 시나리오를 작성할 수도 있지만, **다른 의사소통 집단으로부터 시나리오를 받아(인수) 개발한다**는 의미를 가지고 있다
- 통합 테스트와 얼핏 비슷하다고 생각할 순 있지만, 두 테스트의 차이는 **관점**이다
	- 통합 테스트 : 개발자가 기능에 결함이 없고 제대로 동작하는 지 검증
	- 인수 테스트 : 사용자의 요구사항에 따라 서비스가 제대로 동작하는 지 검증

Java에서는 RestAssured, MockMvc 같은 도구를 활용하여 인수 테스트를 작성할 수 있다.

```java
public static ExtractableResponse<Response> 회원_생성_요청(MeberCreateRequest memberCreateRequest) {
    return RestAssured
            .given()
            .contentType(MediaType.APPLICATION_JSON_VALUE)
            .body(memberCreateRequest)
            .when().post("/api/v1/members")
            .then()
            .extract();
}
```
### 인수 테스트 장점
- 기획자도 코드를 읽을 수 있게 명세서처럼 코드를 작성
	- 개발자, 기획팀 등 서비스 흐름 파악에 도움
- 사용자 테스트를 자동화함으로써 생산성 향상 및 안정감


## Refrence

- [통합 테스트 VS 단위 테스트 VS 인수 테스트](https://tecoble.techcourse.co.kr/post/2021-05-25-unit-test-vs-integration-test-vs-acceptance-test/)
- [통합 테스트](https://needjarvis.tistory.com/443)
- [단위테스트, 통합테스트 그리고 인수테스트](https://jerry92k.tistory.com/m/77)