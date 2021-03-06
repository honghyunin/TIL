#  📚 HTTP 

__HTTP(Hyper Text Transfer Protocol)__ 하이퍼 텍스트 전송 규약. 웹 브라우저를 통해 웹 클라이언트(유저)와 (웹)서버 사이 데이터를 전송하는 프로토콜입니다.

<br>

##  📙 HTTP 특징

- HTTP 클라이언트와 HTTP 서버에 의해서 해석이 됩니다.
- TCP/IP를 이용하는 응용 프로토콜(application protocol)입니다.
- 연결 상태를 유지하지 않는 비연결성 프로토콜입니다.
- 요청/응답(Request/Response) 방식으로 동작합니다.

<br>


## 📘 HTTP 통신 과정

1. 클라이언트가 서버에 HTTP Request(📤)을 합니다.
2. 서버가 사용자의 요청을 받고 HTTP Response(📥)을 한다.

기본적으로 HTTP는 클라이언트의 요청이 없으면 응답하지 않는다.

##  📒 HTTP 상태 코드
   
HTTP 상태 코드는 서버에 요청을 보냈을 때 서버의 상태를 응답으로 보내주는 코드를 의미합니다.

### 1XX 정보

100은 서버가 요청의 일부를 받았으며, 나머지 다른 요청을 더 기다리고 있다는 것을 나타냅니다. 

101은 http에서 https로 프로토콜 전환이 일어났을 때 전환이 승인되었다는 것을 알려줍니다.


### ✔️ 2XX 성공 

- 200은 서버 연결에 성공했다는 의미입니다.


### ↪️ 3XX 리다이렉션 


- 300번대는 페이지를 이동시킬 때 사용합니다.



### 🚫 4XX 클라이언트 오류 

- 400번대는 에러입니다. __400__ 은 서버가 요청을 이해하지 못 할 경우 발생합니다.

- 많이들 보셨던 __404__ 는 찾을 수 없는 페이지입니다. 주소를 잘못 입력했거나 하면 __404__ 를 요청합니다. 403 대신에 404를 전송하는 경우도 있습니다.


### 🚫 5XX 서버 오류


- 500번 부터는 서버 오류입니다. 요청은 의도대로 잘 전송되었지만 서버가 처리하지 못하여 오류가 발생하는 경우입니다. __500__ 은 내부 서버 에러(Internal Server Error)가 발생할 때 전송됩니다.

- __501__ 은 서버에 아직 해당하는 요청 처리 기능을 만들지 않았다는 뜻입니다.


- __503__ 은 서버가 터지거나(트래픽 과부하, Ddos 공격), 유지보수 중일 때 전송됩니다. 


##  📗 HTTP Method

    GET - 데이터 검색 
    POST - 데이터 CRUD를 요청
    OPTIONS - 시스템에서 지원하는 메소드 확인
    HEAD - 응답 시 본문 없이 헤더
    PUT - 전체 수정
    DELETE - 삭제
    PATCH - 일부 수정