# Variable 변수

- Go에서 변수 선언은 이렇게 합니다.

```Go
var name string
```

- 초기값 할당은 다음과 같이 할 수 있습니다.

```Go
var name string = "Hello World"
```

- 선언된 변수는 이렇게 값을 할당합니다.

```Go
name = "Hi!"
```

- Go는 변수의 타입을 지정하지 않고 값으로 타입을 추론하는 기능을 주로 사용합니다.

``` Go
var name = "iam string"
var Integer = "iam integer"
```

- Go에는 변수를 간편하게 선언할 수 있는 Short Assignment Statement (:=)를 사용할 수 있습니다. 하지만 이 표현은 함수 내에서만 사용 가능하고 함수 밖에선 var를 사용해야 합니다.

``` Go
var i = 1
func main(){
    i := 1
}
```

- 📌Go에서는 사용하지 않은 변수를 에러처리 하여 사용하지 않는 변수는 프로그램에서 삭제하도록 해야합니다.


- 📌 Go에서는 변수 선언 시 초기값을 지정하지 않은 경우, int = 0, boolean = false, string = "" 들을 할당합니다.

