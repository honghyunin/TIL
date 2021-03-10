# defer

- Go 의 defer는 함수나 statement 를 제일 후순위로 두어 실행하게 합니다.

``` go
pacakage main

import "fmt"
func main(){
msg := "프로그램이 실행되었습니다"
defer fmt.Println(msg)

    for i:=4 ; i>0 ; i--{
        fmt.Printf("프로그램이 실행되는 중... %d\n", i )
    }
}
/*출력 결과
프로그램이 실행되는 중... 4
프로그램이 실행되는 중... 3
프로그램이 실행되는 중... 2
프로그램이 실행되는 중... 1
끝나써용*/
```
- 위 코드가 실행 되었을 때 defer 키워드를 사용하므로 msg의 아래에 작성된 반복문 보다 나중에 출력되는 결과를 나타냅니다.