# 🌎 HTTP Server start

## ListenAndServe 함수

```go
func ListenAndServe(addr string, handler Handler) error
```
`` 이 함수를 통해 HTTP 서버를 시작하고 HTTP 요청을 받거나, 줄 수 있습니다. ``

`` 이 함수가 error를 반환하면 이 함수 아래 있는 서버(코드)는 실행되지 못합니다.``

- 첫 번째 파라미터는 ``<ip-address>:<port>`` IP 주소와 port를 조합해서 제공하면 되고, 코드 작성 시엔 IP 주소 없이 port 번호만 할당합니다.

- 두 번째 파라미터는 __``Handler``__ 인터페이스의 변수입니다. Handler는 http 요청을 받습니다.

```go
type Handler interface{
    ServeHTTP(ResponseWriter, *Request)
}
```
우리는 직접 ServeHTTP를 직접 구현하여 ListenAndServe에 파라미터로 넘겨줄 수 있습니다.

들어오는 HTTP 요청은 handler argument의 메소드 ServeHTTP의 시작점입니다. ServeHTTP 메소드는 요청 데이터를 받아 응답을 해주는 것이 주요 역할입니다.

``ServeHTTP(res http.ResponseWriter, req *http.Request)``
res arguments는 ResponseWriter 인터페이스입니다.

```go
type ResponseeWriter interface{
    Header() Header
    Write([]byte)(int, error)
    WriteHeader(statusCode int)
}
Write 메소드는 HTTP 응답으로 데이터를 쓴다. 또한 다른 메소드를 사용하여 status Code와 response headers를 넣을 수 있다.
```

req argument는 client에 의해 만들어진 HTTP 요청에 의한 정보가 포함되어 있습니다. Request는 구조체이며 포인터입니다.

```go
Write([]byte) (int ,error)
```
Write는 입력된 byte의 수와 wrtie 함수 사용을 실패하면 에러를 반환합니다.

Writer interface는 Write method를 정의합니다. 그러므로 http.ResponseWriter 인터페이스 객체 res는 Writer 처럼 다룰 수 있습니다. 즉 다형성을 이용할 수 있어 io의 WriteString, fmt의 Fprintf, Fprintf 등을 사용하여 응답할 수 있습니다.

