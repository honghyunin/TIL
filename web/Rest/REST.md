# REST

- REST 는 "Representational State Transfer"의 약자입니다. 월드 와이드 웹과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처의 한 형식이다.
- REST 란 "웹에 존재하는 모든 자원에 고유한 URI를 부여해 활용" 하는 것으로, 자원을 정의하고 자원에 대한 주소를 지정하는 방법론 입니다.
    - 이런 REST 의 형식을 따른 시스템을 RESTful 이라고 부른다.

- HTTP URI 을 통해 자원을 명시하고 HTTP Method 를 통해 해당 자원의 대한 CRUD Operation을 적용한다.

## CRUD Operation, HTTP Method

1. Create : POST(자원생성)
2. Read : GET (자원의 정보 조회)
3. Update : PUT(자원의 정보 업데이트)
4. Delete : DELETE(자원 삭제)

# REST 개념

- HTTP URI(Uniform Resource Identifiter)를 통해 자원(Resource)을 명시하고, HTTP Method를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미합니다.
- REST 는 자원 기반의 구조(Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미합니다. 웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여합니다.

REST 구성요소
1. 자원(Resource)  URL, 

- 모든 자원은 고유한 ID를 가지며, ID는 서버에 존재하고 클라이언트는 각 자원의 상태를 조작하기 위해 요청을 보냅니다.

2. 행위(Verb) , Method

- 클라이언트는 URI를 이용해 자원을 조작하기 위해 Method를 사용합니다. HTTP 프로토콜에서는 ``GET, POST, PUT, DELETE 같은 Method를 제공합니다.``

3. 표현(Representation)

- 클라이언트가 서버로 요청을 보냈을 때 서버가 응답으로 보내주는 자원의 상태를 Representation 이라고 합니다. REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타낼 수 있습니다.

# REST 의 특징

1. 클라이언트 / 서버 구조 (Client-Server)

- 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 됩니다.
- Rest Server : API를 제공하고 비즈니스 로직 처리 및 저장을 책임집니다.
- Client: 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임집니다.

2. 무상태 (Stateless)

- REST는 무상태성을 가집니다. 이는 작업을 위한 상태정보를 따로 저장하고 관리하지 않는다는 의미입니다. 세션 정보나 쿠키 정보를 따로 저장하고 관리하지 않기 때문에 API 서버는 요청만을 단순히 처리하여 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해집니다.

3. 캐시 기능 (Cachealble)

- 웹 표준 HTTP 프로토콜을 그대로 사용하므로 , 웹에서 사용하는 기존의 인프라를 그대로 활용 가능하다.

4. 계층형 구조

    - REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있게 합니다.

5. 인터페이스 일관성(Uniform Interface)

    - URI로 지정한 자원에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다. HTTP 표준에만 따른다면 모든 플랫폼에 사용이 가능하다.

6. 자체 표현 구조
    - (Method) + (URI) 로 이루어져있어 어떤 메서드에 무슨 행위를 하는지 알 수 있으며 REST API 자체가 매우 쉬워서 API 메세지 자체만 보고도 API를 이해할 수 있다.

# REST의 장단점

## 장점
1. 쉬운 사용

HTTP 프로토콜 인프라를 그대로 사용하므로 별도의 인프라를 구축할 필요가 없다.

2. 클라이언트-서버 역할의 명확한 분리

클라이언트는 REST API를 통해 서버와 정보를 주고받는다. REST의 특징인 Stateless에 따라 서버는 클라이언트의 Context를 유지할 필요가 없다.

3. 특정 데이터 표현을 사용가능

REST API는 헤더 부분에 URI 처리 메소드를 명시하고 필요한 실제 데이터를 ‘body’에 표현할 수 있도록 분리시켰다. JSON , XML 등 원하는 Representation 언어로 사용 가능하다.

## 단점
1. 메소드의 한계

REST는 HTTP 메소드를 이용하여 URI를 표현한다. 이러한 표현은 쉬운 사용이 가능하다는 장점이 있지만 반대로 메소드 형태가 제한적인 단점이 있다.

2. 표준이 없음

REST는 설계 가이드 일 뿐이지 표준이 아니다. 명확한 표준이 없다.