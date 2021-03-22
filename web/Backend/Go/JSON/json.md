# JSON



Go에서 JSON을 사용하려면 encoding/json 패키지를 import해야합니다. 아래는 해당 패키지에서 제공하는 JSON 함수입니다.

- func Marshal(v interface{}) ([]byte, error): Go 언어 자료형을 JSON 텍스트로 변환
- func Marshallndent(v interface{}, prefix, indent string)([]byte,error): Go 언어 자료형을 JSON 텍스트로 변환하고 사람이 보기 편하도록 들여쓰기를 해줌
- func Unmarshal(data []byte, v interface{}) error: JSON 텍스트를 Go 언어 자료형으로 변환

 

# Key-Value 구조 JSON

## JSON 직렬화
아래는 맵 형태의 데이터를 JSON 형태로 변환하는 방법입니다.

```go
package main
import(

"encoding/json"

"fmt"

)

func main(){

data := make(map[string]interface{}) *// 문자열을 키 로 하고 모든 자료형을 저장할 수 있는 맵 생성*

data["name"] = "kim"

data["age"] = 25

doc , _ := json.Marshal(data) *// 맵을 JSON 문서로 변환*

fmt.Println(string(doc)) *// age {"age":25, "name":"kim"}: 문자열로 변환하여 출력*

}

*// {"age":25, "name":"kim"}:*
```
````

- 문자열을 키로하고 모든 자료형을 값으로 저장할 수 있는 맵을 할당합니다. 그리고 적절히 데이터를 대입한 뒤 json.Marshal 함수를 사용하여 JSON 문서로 변환합니다. json.Marshal 함수에서 리턴된 값은 []byte 형식이므로 출력할 때는 string 형식으로 반환해줍니다. JSON 문서로 변환했을 때 한 줄로 붙어서 나오면 사람이 읽기 힘듭니다. 따라서 다음과 같이 json.Marshallndent 함수를 사용하면 사람이 쉽게 읽을 수 있도록 변환할 수 있습니다.
````

```go
doc, _ := json.MarshalIndent(data, "","		")

#결과
{
	"age":10,
	"name": "maria"
}
```

`` ``

- 첫 번째 매개변수는 JSON 문서로 만들 데이터입니다. 
- 두 번째 매개변수는 JSON 문서의 첫 칸에 표시할 문자열(Prefix)인데 보통 **""**( 빈문자)를 지정합니다. 
- 세 번째 매개변수는 들여쓰기할 문자입니다. 공백 문자나 탭 문자를 사용할 수 있습니다. Prefix는 표시하지 않고, 들여쓰기는 2칸으로 지정하면 다음과 같이 JSON 문서로 변환됩니다.


# JSON 역직렬화
아래는 JSON 형태를 Go에서 받아 읽는 방법입니다.

```go
package main
import(
"encoding/json"
"fmt"
)
func main(){
	doc :=
	{
		"name":"kim",
		"age":25
}

var data map[string]interface{} // JSON 문서의 데이터를 저장할 공간을 맵으로 선언
json.Unmarshal([]byte(doc), &data) // doc를 바이트 슬라이스로 변환하여 넣고, data의 포인터를 넣어줌
fmt.Println(data["name"], data["age"]) // kim 25: 맵에 키를 지정하여 값을 가져옴
}
```
