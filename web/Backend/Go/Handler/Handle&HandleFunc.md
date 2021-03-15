# Handle / HandleFunc

Go에서 기본적인 서버를 구동시키기 위해 HandleFunc(), HandlerFunc() 함수를 사용한다.

```go
package main
import (
	"io"
	"net/http"
)
func a(res http.ResponseWriter, req *http.Request){
	io.WriteString(res, "hello world")
}
func main() {
	http.HandleFunc("/", a)
	http.ListenAndServe(":8080",nil)
}
```

- 위 코드는 golang을 이용한 웹 프로그래밍의 hello world입니다.

- 위 코드를 실행시키면 [localhost:8080/](http://localhost:808/) 주소로 들어가면 hello world가 찍혀있는 걸 볼 수 있습니다.

```go
package main
import (
	"io"
	"net/http"
)
func a(res http.ResponseWriter, req *http.Request){
	io.WriteString(res, "hello world")
}
func main() {
	http.Handle("/bye", http.HandlerFunc(a))
	http.ListenAndServe(":8080",nil)
}
```

- 위 예제는 첫 예제와 다르게 __http.HandleFunc__ 대신 __http.Handle__ 함수를 사용하였습니다.

- http.Handle의 두 번째 인자를 보시면 __http.HandlerFunc__ 라는 함수가 사용되었습니다.

## Handler 와 HandlerFunc 의 차이점

`` http.HandlerFunc 와 http.Handle의 차이점 중에 하나는 두번째 인자의 타입에 있습니다. ``
`` HandleFunc의 경우 위에서 말했듯이 두 번째 인자로 func(http.ResponseWriter, *http.Request)형태로 이루어져 있는 함수를 받습니다. ``

```go
	func Handle(pattern string,handler Handler)
```

- Handle의 경우 Handler type을 받습니다.


```go
	type Handler interface{
		ServeHTTP(ResponseWriter, *Request)
	}
```

위 코드는 Handler 란 interface를 정의한 것이고 ServeHTTP 함수를 정의해야 Handler interface가 됩니다.

```go
	func a(res http.ResponseWriter, req *http.Request){
		i.oWriteString(res, "bye world")
	}
```

위 a 함수가 http.Handle의 두 번째 인자로 들어가기 위해선 a 함수가 Handler interface가 되어야하는데 이걸 도와주는 게 http.HandlerFunc함수입니다.

![handlerfunc](/images/handlerfunc.png)

- 사진을 보면 나와있듯이 HandlerFunc type은 ServeHTTP 함수를 가지고 있고 이는 handlerFUn type은 Handler interface란 뜻입니다.

- HandlerFunc(a)를 하면 함수 a는 결국 Handler interface가 되기 때문에 작동되는 것입니다.


## 결론

- Handler 은 경로별로 요청을 처리할 핸들러를 등록하는 것이고,

- HandlerFunc 은 경로별로 요청을 처리할 핸들러 함수를 등록하는 것입니다.