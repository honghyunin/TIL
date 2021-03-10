# recover

- Go의 내장함수인 ``recover()`` 함수는 __panic 함수에 의한 패닉상태를 다시 정상상태로 되돌리는 함수__ 이다. panic 예제에서는 main 함수의 println()이 호출되지 못하고 프로그램이 강제 종료 되었지만, 아래 예제와 같이 recover 함수를 사용하면 panic 상태를 제거하고 panicTest() 아래의 println() 을 호출하게 된다.

``` go
package main

import "fmt"

func panicTest() {
	var a = [3]int{1,2,3}

    defer func(){
        if r := recover(); r != nil{
            fmt.Println("OPEN ERROR", r)
        }()
    }
	
	defer fmt.Println("Panic done")
	
	for i := 0; i < 5; i++ {
		fmt.Println(a[i])
	}		
}

func main() {
	panicTest()

	fmt.Println("실행되고 싶다!")
}
```
