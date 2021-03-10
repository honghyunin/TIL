# string

- Go에서는 문자열은 string 으로 표현합니다.

- 문자열 리터럴은  ``, "" 로 표현 가능합니다.
    - Back Quote `` 내부에 있는 문자열은 Raw String Literal 이라 부르며, Raw String 그대로 값을 갖게 됩니다.

    - 이중인용부호 "" 내부에 있는 문자열은 Interpreted String Literal 이라 부르며, 하나의 라인에서만 사용이 가능합니다.내부에 Escape 문자열은 각각의 의미로 해석됩니다. 

``` Go
func main() {
    rawLiteral := `가나다\n라마바\n`
    
    interLiteral := "가나다\n라마바"

    reinterLiteral := "가나다\n라마바" + "아자차\n카파타"

}

출력내용 :

가나다\n라마바\n

가나다
라마바

가나다
라마바아자차
카파타
```