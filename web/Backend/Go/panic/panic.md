# panic

- Go의 내장함수인 ``panic()`` 함수는 __``현재 함수를 즉시 멈추고 현재 함수에 있는 defer 함수들을 모두 실행한 후 즉시 리턴합니다.``__ 이러한 panic 모드 실행 방식은 다시 상위함수에도 똑같이 적용되고, 계속 콜스택을 타고 올라가며 적용된다. 그리고 마지막에는 프로그램이 에러를 내고 종료하게 됩니다.

``` go
package main

import "fmt"

func panicTest() {
	var a = [3]int{1,2,3}
	
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