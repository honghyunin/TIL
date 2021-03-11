# Go 에러

- Go는 내장 타입으로 error라는 interface 타입을 갖습니다.  
- Go 에러는 이 인터페이스를 통해서 주고 받게 되어 이 interface는 다음과 같은 하나의 메서드를 갖습니다. 개발자는 이 인터페이스를 구현하는 커스텀 에러 타입을 만들 수 있습니다.

```go
type error interface{
    Error() string
}
```

## Go 에러처리

Go 함수가 결과와 에러를 함께 리턴한다면, 이 에러가 nil 인지를 확인할 수 있습니다. os.Open() 함수는 func Open(name string)(file *File, err error) 과 같은 함수 원형을 갖는 것으로 첫 번째는 File 포인터를 두 번째는 error 인터페이스를 리턴합니다. 그래서 이 경우 두 번째 error를 체크해서 nil 이면 에러가 없는 것이고, nil이 아니면 err.Error()로 부터 해당 에러를 알 수 있습니다. 아래 예제는 파일을 오픈하는데 에러가 발생하면 에러메시지를 출력하고 빠져나가는 예입니다.

```go
package main
 
import (
    "log"
    "os"
)
 
func main() {
    f, err := os.Open("C:\\temp\\1.txt")
    if err != nil {
        log.Fatal(err.Error())
    }
    println(f.Name())
}
```

또 다른 에러처리로서 error의 Type을 체크하여 에러 타입별로 에러 처리를 하는 방식이 있습니다. 아래 예제에서 otherFunc()를 호출한 후 error가 err로 리턴되었을 때, 이 err의 타입별로 다른 처리를 하는 것을 볼 수 있습니다 (switch 문에서 변수명.(type)의 방식으로 타입 체크를 한다). 디폴트의 경우 에러타입이 nil인 경우 에러가 없는 경우이고, 에러가 있으면 다음 case문에서 그 에러타입이 MyError인지를 체크하고, 아니면 다음 case에서 일반 에러 케이스를 처리합니다. 모든 에러는 error 인터페이스를 구현하므로 마지막 case문은 모든 에러에 적용됩니다.

``` go
_, err := otherFunc()
switch err.(type) {
default: // no error
    println("ok")
case MyError:
    log.Print("Log my error")
case error:
    log.Fatal(err.Error())
}
```