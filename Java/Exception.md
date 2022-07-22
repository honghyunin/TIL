# Exception 예외란 ?
> 입력 값에 대한 처리가 불가능하거나, 프로그램 실행 중에 참조된 값이 잘못된 경우 등 정상적인 프로그램의 흐름을 어긋나는 것을 말한다.

## Checked Exception

- 반드시 명시적 예외처리를 해야하며, 처리하지 않으면 컴파일 시점에서 예외가 발생합니다.
- Error와 RuntimeException을 상속하지 않은 클래스들이 Checked Exception 입니다.


## Unchecked Exception

- CheckException과 반대로 RuntimeException을 상속받는 모든 클래스가 Unchecked Exception입니다.
- 명시적인 예외처리를 강제 하지 않기 때문에 UncheckedException입니다. 따라서 try ~ catch 나, 메서드 throw 단에서 처리합니다.

![exception](/images/exception.png)