# Goroutine

- Go루틴은 Go 런타임이 관리하는 Lightweight 논리적(혹은 가상적) 쓰레드이다. Go에서 __``go``__ 키워드를 사용하여 goroutine을 실행하면, ``goroutine은 비동기적으로(asynchronously)함수루틴을 실행``하므로, __``여러 코드를 동시에(Concurrently) 실행하는데 사용됩니다.``__
- 고루틴들은 여러개의 스레드에 다중화(multiplex) 됩니다. 하나의 스레드에선 하나의 고루틴이 실행되고 실행중인 고루틴이 또 블록되면 또 다른 고루틴이 스레드에서 실행됩니다. 이러한 고루틴의 스케쥴링과 OS로부터의 스레드 할당은 Go 런타임이 대신 하기 때문에 개발자는 스레드 관리를 신경 쓰지 않아도 됩니다.

## 고루틴 사용법

- 함수 앞에 __``go``__ 키워드를 붙임으로 고루틴을 실행시킬 수 있습니다. 
``` Go
go db.con()
```

- 함수 리터럴은 고루틴 호출에 유용할 수 있습니다.

``` Go
func Announce(message string, delay time.Duration) {
    go func() {
        time.Sleep(delay)
        fmt.Println(message)
    }()
}
```
- Go 에서 함수 리터럴은 클로져입니다. 따라서 함수에 의해 참조된 변수들은 함수들이 활성화되는 동안 생존할 수 있습니다. 위 예시에선 고루틴으로 실행되는 익명함수에서 자신의 범위 밖의 변수인 __``delay``__  와 __``message``__ 를 참조하고 있습니다.
