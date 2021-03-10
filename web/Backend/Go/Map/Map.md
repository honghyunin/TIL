# Map

- Map 은 키(Key)에 대응하는 값(Value)을 신속히 찾는 해시테이블(Hash table)을 구현한 자료구조입니다. 

- Map은 __``map[KeyType]ValueType``__ 과 같이 선언할 수 있습니다. 예를 들어 정수를 키로하고 문자열을 값으로 하는 맵 변수 idMap을 선언하기 위해서는 다음과 같이 작성할 수 있습니다.

``idMap = make(map[int]string)``

- 이때 선언된 변수 idMap은 (map은 reference 타입이기에) nill 값을 갖으며, 이를 Nill Map이라 부릅니다. Nill map에는 어떠 데이터를 쓸 수 없는데, map을 초기화 하기 위해 make() 함수를 사용할 수 있습니다.

``idMap = make(map[int]string)``
- make() 함수의 첫 번째 파라미터로 map 키워드와 [키타입]값타입을 지정하는데, 이때의 make() 함수는 해시테이블 자료구조를 메모리에 생성하고 그 메모리를 가리키는 map value를 리턴합니다.(map value는 내부적으로 구조체를 가리키는 포인터입니다) 따라서 idMap 변수는 이 해시테이블을 가리키는 map을 가리키게 됩니다.

- map은 ``make()`` 함수를 써서 초기화할 수도 있지만, 리터럴(literal)을 사용해 초기화할 수도 있다. 리터럴 초기화는 ``map[keyType]ValueType { Key:value}`` 와 같이 ``Map 타입 뒤 { } 괄호 안에 "키: 값" 들을 열거`` 하면 된다.

```go
tickers := map[string]string{
    "ASHISLAND": "윤진영",
    "BIG_Naughty":"서동현",
    "Chin":"안상진",
}
```
## Map 사용 방법

- map이 ``make()`` 함수에 의해 갓 초기화 되었을 때는, 아무 데이터가 없는 상태입니다. 이때 새로운 데이터를 추가하기 위해서는 ``map변수[키] = 값`` 과 같이 해당 키에 그 값을 할당하면 됩니다. 예를 들면, 아래 예제에서 ``키 901에 Apple을 할당하면 새 해시 키-값 쌍이 추가됩니다. 만약 키 901의 값이 이미 존재했다면, 추가대신 값만 갱신합니다.``

```go
package main
func main(){
    var m map[int]string
    m = make(map[int]string)
    m[503] = "Chicken"
    m[134] = "Dog"
    m[777] = "Cat"
    str := m[777]
    println(str)
    noData := m[503]
    println(noData)
    delete(m,134)
}
```

- map에서 특정 키에 대해 값을 읽을 때는 ``map변수[키]`` 를 읽으면 됩니다. 위 예제에서 m[134]는 Dog라는 값을 str 변수에 할당하게 됩니다. 만약 map안에 찾는 키가 존재하지 않고 reference 타입인 경우 nil을 value 타입인 경우 zero를 리턴합니다.

- map에서 ``특정 키와 그 값을 삭제`` 하기 위해서는 ``delete()`` 함수를 사용합니다.

## Map 키 체크

- map을 사용할 때 map안에 키가 존재하는 지를 체크할 필요가 있습니다. 이를 위해 Go에선 "map변수[키]" 읽기를 수행할 때 2개의 리턴값을 리턴합니다. 첫 번째는 키에 상응하는 값이고, 두 번째는 그 키가 존재하는 지 아닌지를 나타내는 bool 값입니다. 즉   

```go
package main
func main(){
    tickers := map[string]string{
    "ASHISLAND": "윤진영",
    "BIG_Naughty":"서동현",
    "Chin":"안상진",
	}
    val, exists := tickers["ASHISLAND"]
    if !exists {
        println("No ASHISLAND ticker")
    } else{
		println(val)
	}
}
```

## for 루프를 사용한 Map 열거

- Map이 갖고 있는 모든 요소들을 출력하기 위해 for range 루프를 사용합니다. Map 컬렉션에 for range를 사용하면, Map 키와 값 2개의 데이터를 리턴한다. 아래 예제는 for 루프를 사용하여 맵으로부터 Key와 Value를 하나씩 가져와서 출력하는 코드입니다.

```go
package main
import "fmt"
func main(){
    myMap := map[string]string{
        "가":"가락",
        "나":"나락",
        "다":"다락",
    }
    for key, val := range myMap{
        fmt.Println(key, val)
    }
}
```
