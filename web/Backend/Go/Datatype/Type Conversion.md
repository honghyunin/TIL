# Type Conversion

- Go 에서는 지정된 타입을 다른 타입으로 변환하기 위해서는 T(v)와 같이 표현하고 이를 Type Conversion 이라고 부릅니다. 여기서 T는 변환하고자 하는 타입을 표시하고, v는 변환될 값(value)을 지정한 것입니다.

```go
func main(){
    var i int = 777
    var u uint = uint(i)
    var f float16 = float16(i)
    str := "가나다"
    bytes := []byte(str)
    str2 := string(bytes)
    println(bytes, str2)
}
```
