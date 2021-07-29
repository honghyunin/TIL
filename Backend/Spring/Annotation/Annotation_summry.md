# Annotation / method

## @PostConstruct

- 의존성 주입이 끝난 뒤 실행될 메소드에 적용해야한다
- 의존성 주입이 이루어진 후 초기화를 수행하는 메소드이다.
- 다른 리소스에서 호출되지 않아도 수행된다

## @AllArgsConstructor

- 모든 필드를 파라미터에 필드 값을 받는 생성자를 만들어준다

## @Valid

- 필드에 적용된 검증조건을 거치고 요청을 받는 어노테이션

## @RestController

- 컨트롤러를 JSON을 반환하는 컨트롤러로 만들어 줍니다.
- 에전에는 @ResponseBody를 각 메소드마다 선언했던 것을 한번에 사용할 수 있게 해준다고 생각하면 됩니다.

## @RequestParam

- url상에서 '?variable=value' 형식으로 들어온 parameter를 받는 annotation 이다.

## @RequestBody

- HTTP 요청을 자바 객체로 전달 받을 수 있도록 함

## @ResponseBody

- 자바 객체를 HTTP 응답 몸체로 전송할 수 있음.

## @GetMapping

- HTTP Method인 Get의 요청을 받을 수 있는 API를 만들어줌
- 예전에는 @RequestsMapping(method = RequestMethod.GET)으로 사용되었습니다. 이제 이 프로젝트는 /hello 로 요청이 오면 문자열 hello를 반환하는 기능을 가지게 되었습니다.

## @Autowired

- 스프링이 관리하는 빈(Bean)을 주입 받습니다.

## @private MockMvc mvc

- 웹 API를 테스트할 때 사용합니다.
- 스프링 MVC 테스트의 시작점입니다.
- 이 클래스를 통해 HTTP GET, POST 등에 대한 API 테스트를 할 수 있습니다.

## mvc.perform(get("/hello"))

- MockMvc를 통해 /hello 주소로 HTTP GET 요청을 합니다.
- 체이닝이 지원되어 아래와 같이 여러 검증 기능을 이어서 선언할 수 있습니다.

## .andExpect(status().isOk())

- mvc.perform의 결과를 검증합니다.
- HTTP Header의 Status를 검증합니다.
- 우리가 흔히 알고 있는 200, 400, 500 등의 상태를 검증합니다.
- 여기선 OK 즉, 200인지 아닌지를 검증합니다.

## .andExpect(content().string(hello))

- mvc.perform의 결과를 검증합니다.
- 응답 본문의 내용을 검증합니다.
- Controller에서 "hello"를 리턴하기 때문에 이 값이 맞는 지 검증하니다.

## @assertThat

- assertj 라는 테스트 검증 라이브러리의 검증 메소드입니다.
- 검증하고 싶은 대상을 메소드 인자로 받습니다.
- 메소드 체이닝이 지원되어 isEqualTo와 같이 메소드를 이어서 사용할 수 있습니다.

## @isEqualTo

- assertj의 동등 비교 메소드입니다.
- assertThat에 있는 값과 isEqualTo의 값을 비교해서 같을 때만 성공입니다.

## @param

- API 테스트할 때 사용될 요청 파라미터를 설정합니다.
- 단, 값은 String만 허용됩니다.
- 그래서 숫자/날짜 등의 데이터도 등록할 때는 문자열로 변경해야만 가능합니다.

## @jsonPath

- JSON 응답 값을 필드별로 검증할 수 있는 메소드입니다.
- $를 기준으로 필드명을 명시합니다.
- 여기서는 name과 amount를 검증하니 $.name, $.amount로 검증합니다.

## @After

- Junit에서 단위 테스트가 끝날 때마다 수행되는 메소드를 지정
- 보통은 배포 전 전체 테스트를 수행할 때 테스트간 데이터 침범을 막기 위해 사용합니다.
- 여러 테스트가 동시에 수행되면 테스트용 데이터베이스인 H2에 데이터가 그대로 남아 있어 다음 테스트 실행 시 테스트가 실패할 수 있습니다.

## @postsRepository.save

- 테이블에 posts에 insert/update 쿼리를 실행합니다.
- id 값이 있다면 update가, 없다면 insert 쿼리가 실행됩니다.

## @postsRepository.findAll

- 테이블에 posts에 있는 모든 데이터를 조회해오는 메소드입니다.

## @SpringBootTest

- 이 어노테이션을 사용할 경우 **H2 데이터베이스**를 자동으로 실행해줍니다
- 

# Lombook

## @NoArgsConstructor

- 기본 생성자 자동 추가
- public Posts(){}와 같은 효과

## @Getter

- 선언된 모든 필드의 get 메소드를 생성해줍니다.

## @RequiredArgsConstructor

- 선언된 모든 final 필드가 포함된 생성자를 생성해줍니다.
- final이 없는 필드는 생성자에 포함되지 않습니다.

## @Builder

- 해당 클래스의 빌더 패턴 클래스를 생성
- 생성자 상단에 선언 시 생성자에 포함된 필드만 빌더에 포함

## @RequiredArgsConstructor

- final이 선언된 모든 필드를 인자값으로 하는 생성자를 만들어 줌

→ 롬복 어노테이션을 사용한 이유는 해당 클래스의 의존성 관계가 변경될 때마다 코드를 수정해야하는 번거로움을 해결하기 위함.

## @Entity

- 테이블과 링크될 클래스임을 나타냄
- 기본값으로 클래스의 카멜케이스 이름을 언더스코어 네이밍(_)으로 테이블 이름을 매칭
- ex) [SalessManager.java](http://salessmanager.java) → sales_manager table

## @Id

- 해당 테이블의 PK 필드를 나타냄

## @GenerateValue

- PK의 생성 규칙을 나타냄
- 스프링 부트 2.0 에선 GenerationType.IDENTITY 옵션을 추가해야만 auto_increment가 됨

## @Column

- 테이블의 칼럼을 나타내며 굳이 선언하지 않더라도 해당 클래스의 필드는 모두 칼럼이 된다
- 사용하는 이유는, 기본값 외에 추가로 변경이 필요한 옵션이 있으면 사용함
- 문자열의 경우 varchar(255) 가 기본값인데, 사이즈를 500으로 늘리고 싶거나, 타입을 TEXT로 변경하고 싶거나 등의 경우에 사용됨