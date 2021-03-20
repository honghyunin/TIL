# 패키지 Import

- 타 패키지를 프로그램에서 사용하기 위해서는 ``import``를 사용하여 패키지를 포함시킵니다.

``` go
package main
import "fmt"
func main(){
    fmt.Println("hello")
}
```

- 패키지를 import 할 때, Go 컴파일러는 GOROOT 혹은 GOPATH 환경변수를 검색합니다. 그러나 표준 패키지는 GOROOT/pkg 에서, 사욪아 패키지나 3rd Party 패키지의 경우 GOPATH/pkg에서 패키지를 찾게 됩니다.

- GOROOT는 자동으로 설정되지만, GOPATH는 사용자가 지정해주어야 합니다.
