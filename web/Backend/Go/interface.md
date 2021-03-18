# Interface

- ``interface는 메서드들의 집합체``입니다. interface는 메서드의 헤드만 구현하여 메서드의 원형(Prototype)들을 정의합니다. 하나의 interface를 구현하기 위해서는 그 인터페이스가 갖는 모든 메서드를 구현하면 됩니다.
- __인터페이스는 구조체와 마찬가지로 type 문을 사용하여 정의합니다.

```go
type Shape interface {
    area() float64
    perimeter() float64
}
```
# 인터페이스 구현
- 인터페이스를 구현하기 위해서 해당 타입 인터페이스의 메서드들을 모두 구현하면 되므로, 위의 Shape 인터페이스를 구현하기 위해서는 ``area()``, ``perimeter()`` 2개의 메서드만 구현하면 됩니다. 예를 들어 type_1과 type_2 라는 2개의 타입이 있을 때, Shape 인터페이스를 구현하기 위해서는 아래와 같이 각 타입별로 2개의 메서드를 구현해 주면 됩니다.

```go
//type_1 정의
type type_1 struct{ 
    width, height float64
}

//type_2 정의
type type_2
struct{
    cm float64
}
//Rect 정의
type Rect struct {
    width, height float64
}
 
//Circle 정의
type Circle struct {
    radius float64
}
 
//Rect 타입에 대한 Shape 인터페이스 구현 
func (r Rect) area() float64 { return r.width * r.height }
func (r Rect) perimeter() float64 {
     return 2 * (r.width + r.height)
}
 
//Circle 타입에 대한 Shape 인터페이스 구현 
func (c Circle) area() float64 { 
    return math.Pi * c.radius * c.radius
}
func (c Circle) perimeter() float64 { 
    return 2 * math.Pi * c.radius
}
```

# 인터페이스 사용
- 인터페이스를 일반적으로 사용하는 예시로 함수가 파라미터를 통해 인터페이스를 받아들이는 경우를 들 수 있습니다. ``함수 파라미터가 interface 인 경우, 이는 어떤 타입이든 해당 인터페이스를 구현하기만 하면 모두 입력 파라미터로 사용될 수 있다는 것을 의미``합니다.

- 아래 예제에서 ``showArea()`` 함수는 Shape 인터페이스들을 파라미터로 받아들이고 있는데, 따라서 Rect와 Circle 처럼 Shape 인터페이스를 구현한 타입 객체들을 파라미터로 받을 수 있습니다. ``showArea()`` 함수 내에서 해당 인터페이스가 가진 메서드 즉 ``area()`` 혹은 ``perimeter()``를 사용할 수 있습니다.

```go
func main() {
    r := Rect{10., 20.}
    c := Circle{10}
 
    showArea(r, c)
}
 
func showArea(shapes ...Shape) {
    for _, s := range shapes {
        a := s.area() //인터페이스 메서드 호출
        println(a)
    }
}
```

# 인터페이스 타입
- Go 프로그래밍을 하다 보면 흔히 ``빈 인터페이스(empty interface)``를 자주 접하게 되는데요, 흔히 ``인터페이스 타입(interface type)으로도 불리웁니다.`` 예를 들어 표준 패키지들의 함수 Prototype을 살펴보면,  빈 interface가 자주 등장함을 볼 수 있습니다. __빈 interface는 interface{} 와 같이 표현__ 합니다.

```go
func Marshal(v interface{}) ([]byte, error);

func Println(a ...interface{})(n int, err error);
```
-  __``Empty interface``__ ``는 메서드를 전혀 갖지 않는 빈 인터페이스``로서, Go의 모든 Type은 적어도 0개의 메서드를 구현하여, 흔히 ``Go에서 모든 Type을 나타내기 위해 빈 인터페이스를 사용``합니다. 즉, __``빈 인터페이스는 어떠한 타입도 담을 수 있는 컨테이너``__ 라고 볼 수 있으며, 여러 다른 언어에서 흔히 일컫는 Dynamic Type 이라고 볼 수 있습니다. (empty interface는 C#, Java에서 object라 볼 수 있으며, C/C++ 에서는 void*와 같다고 볼 수 있습니다)

- 아래 예제에 ``인터페이스 타입 x는 정수 1을 담았다가 다시 문자열 Tom을 담고 있는데,
실행 결과는 마지막에 담은 Tom을 출력``합니다.

```go
package main
 
import "fmt"
 
func main() {
    var x interface{}
    x = 1 
    x = "Tom"
 
    printIt(x)
}
 
func printIt(v interface{}) {
    fmt.Println(v) //Tom
}
```

# Type Assertion

- Type Assertion은 인터페이스가 가지고 있는 실제 값(concrete value)에 접근할 수 있게 해줍니다.
( golang의 인터페이스는 임의의 타입 값을 가질 수 있습니다.)

```go
var n interface{} = 15
var := n.(Int)
```
- 위 코드에서 우리들은 n의 interface 값이 실제로는 int타입임을 알 수 있습니다.
따라서 Type assertion을 이용하여 n의 실제 값에 접근할 수 있습니다.

- 어떤 인터페이스 값이 특정 타입인지를 확인하기 위해 ok 값을 받을 수도 있습니다.
``` go
v, ok := n.(int)
```
- 만약 n의 타입이 int가 아니라면 v는 int의 zero value인 0이 될 것이고, ok는 false 가 될 것입니다.
