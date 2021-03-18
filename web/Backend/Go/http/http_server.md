# 🌎 HTTP Server start

## net/http Package func

-  ``func ListenAndServe(addr string, handler Handler) error``: HTTP 연결을 받고, 요청에 응답
- ``func HandleFunc(pattern string, handler func(ResponseWriter, *Request))``: 경로별로 요청을 처리할 핸들러 함수를 등록
- ``func Handle(pattern string, handler Handler)`` : 경로별로 처리할 핸들러를 등록
- ``func FileServer(root FileSystem) Handler``: 파일 서버 핸들러를 등록
- ``func StripPrefix(prefix string, h Handler) Handler``: HTTP 요청 경로에서 특정 문자열을 제거한다. 예) /go/server.go -> server.go
- ``func NewServeMux() *ServeMux``: HTTP 요청 멀티플렉서 인스턴스 생성

먼저 간단하게 Hello World! 를 출력해보겠습니다

```go
package main
import (
    "net/http"
)
func main(){
    http.HandleFunc("/", func(res http.ResponseWriter, req *http.Request){
        res.Write[]byte("Hello, World!")) // 웹 브라우저에 응답합니다
    }) // "/" 경로에 접속했을 때 실행할 함수 설정
    http.ListenAndServe(":3000", nil)
}
```

- http.HandleFunc에 URL 하위 경로와 해당 경로를 처리할 함수를 설정해줍니다. 여기서 경로는 "/"를 설정했으므로 웹 브라우저에서 이 경로로 접속했을 때 두 번째 매개변수에 있는 함수가 실행됩니다. 

- http.ListenAndServe 함수에 포트 번호를 지정하여 웹 서버를 실행합니다. 앞에서 핸들러를 설정했으므로 두 번째 매개변수는 nil 로 설정합니다.

<br>

`` 이번에는 `` __``http.ListenAndServe``__ ``함수에 핸들러를 넣어서 웹 서버를 실행해보겠습니다. ``

```go
package main
import(
    "net/http"
)
func main() {
    mux := http.NewServeMux() // HTTP 요청 멀티플렉서 생성

    mux.HandleFunc("/", func(res http.ResponseWriter, req *http.Request){
        res.Write([]byte("hello, world!")) // 웹 브라우저에 응답
    })
    http.ListenAndServe(":3000", mux) // 3000번 포트에 웹 서버를 실행하고, mux를 이용하여 HTTP 요청을 처리
}
```

- 먼저 __http.NewServeMux__ 함수로 HTTP 요청 멀티플렉서(multiplexer) 인스턴스를 생성합니다. URL 경로를 동시에 여러개를 처리하여 HTTP 요청 멀티플렉서라 부릅니다(앞서 사용한 __http.HandleFunc__ 함수도 내부적으로는 __http.NewServeMux__ 로 __DefaultServeMux__ 인스턴스를 생성하여 사용하므로 완전히 같은 기능입니다.)

- HTTP 요청 멀티플렉서 인스턴스의 __HandleFunc__ 함수에서 URL 하위 경로와 해당 경로를 처리할 함수를 설정해주면 됩니다. ( 사용 방법은 앞의 http.HandleFunc 함수와 같습니다.)