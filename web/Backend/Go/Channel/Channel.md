
## 채널 (Channel)

- Go채널은 데이터를 주고 받는 통로라고 할 수 있습니다. ``채널은 make() 함수를 통해 미리 생성되어야 하며, 채널 연산자 <-``을 통해 데이터를 주고 받습니다. 채널은 goroutine을 통한 데이터 교환 시에 주로 사용되는데, 대상이 준비될 때까지 채널에서 대기함으로써 별도의 lock을 걸지 않고 데이터를 동기화하는데 사용됩니다.

- 아래 예제는 정수형 채널을 생성하고 goroutine에서 채널로 string 형의 데이터를 받는 코드입니다.

```Go
   ch := make(chan string)

   go func(){
      ch <- "메시지" // 채널에 "메시지"를 보낸다
   }()

   var t string
   t = <- ch // 채널로부터 "메시지"를 받는다
   fmt.Println(t)
```

## Go 채널 버퍼링

- Go 에는 2가지의 채널이 있습니다. ``Unbuffered Channel``과 ``Buffered Channel``이 있습니다. Go 채널은 Unbuffered Channel 로써 이 채널에선 ``하나의 수신자가 데이터를 보내는 채널에 묶여 있게 된다.`` 하지만, Buffered Channel을 사용하면 비록 ``수신자가 받을 준비가 되어 있지 않을 지라도 지정된 버퍼만큼 데이터를 보내고 계속 다른 일을 수행할 수 있다.`` 버퍼 채널은 make(chan type, N) 함수를 통해 생성되는데, 두 번째 파라미터 N에 사용할 버퍼 갯수를 넣습니다. 예를 들어, make(chan int, 10)은 10개의 정수형을 갖는 버퍼 채널을 만든다.

- 버퍼 채널을 이용하지 않는 경우 아래 코드는 에러 ``(fatal error: all goroutines are asleep - deadlock!)``를 발생시킨다. 왜냐하면 메인루틴에서 채널에 1을 발송하면서 수신자를 기다리고 있는데, 이 채널을 받는 수신자 Go루틴이 없기 때문입니다.

```Go

package main
import "fmt"
func main(){
   s := make(chan string)
   s <- "메시지"
   fmt.Println(<-s)
}
```

- 허나 아래와 같이 버퍼 채널을 사용하면, __``수신자가 당장 없더라도 최대버퍼 수까지 데이터를 보낼 수 있으므로 에러가 발생하지 않는다.``__

``` go
package main
import "fmt"
func main(){
   s := make(chan string, 1)
   //수신자가 없더라도 보낼 수 있습니다.
   s <- "메시지"
   fmt.Println(<-s)
}
```

## 채널 파라미터

- 채널을 함수의 파라미터로 전달할 때, 일반적으로 송수신을 모두 하는 채널을 전달하지만, 특별히 해당 채널로 오직 송신 / 수신만 할 것인지를 지정할 수도 있다. `` 송신 파라미터는 (p chan <- int)와 같이 chan <- 을 사용``하고, ``수신 파라미터는 (p <- chan int)와 같이 <-chan을 사용``한다. 만약 송신 채널 파라미터에서 수신을 한다거나, 수신 채널에서 송신을 하게 되면, 에러가 발생한다.

# 채널 닫기

- 채널을 오픈한 후 데이터를 송신한 후, ``close()`` 함수를 사용하여 채널을 닫을 수 있습니다. __``채널을 닫게 되면, 해당 채널로는 더 이상 송신을 할 수 없지만, 채널이 닫힌 이후에도 계속 수신은 가능합니다.``__ 채널 수신에 사용되는 ``<- ch`` 은 두 개의 리턴값을 갖는데, ``첫째는 채널 메시지이고``, ``두 번째는 수신이 제대로 되었는 가를 나타냅니다.`` 만약 채널이 닫혔다면 두 번째 리턴값은 false를 리턴합니다.

``` Go
package main
func main(){
   ch := make(chan string, 2)
   // 채널에게 송신합니다
   ch <- 1
   ch <- 2
   // 채널을 닫아줍니다
   close(ch)
   // 채널을 수신합니다
   println(<-ch)
   println(<-ch)
   if _, success := <-ch; !success {
      println("더 이상 데이터가 없습니다")
   }
}
```

## 채널 range문

- ``채널에서 송신자가 송신을 한 후, 채널을 닫을 수 있다. 그리고 수신자는 임의의 갯수의 데이터를 채널이 닫힐 때까지 계속 수신할 수 있다.`` 아래 예제는 이러한 송수신 방법을 표현한 것으로, __수신자는 채널이 닫히는 것을 체크하면서 계속 루프를 돌게 됩니다.__
- 방법 1 ``무한 for 루프 안에서 if 문으로 수신 채널의 두 번째 파라미터를 체크하면 수신을 종료하게 됩니다.``
- 방법 2``채널 range문은 range 키워드 다음의 채널로부터 계속해서 수신하다가 채널이 닫힌 것을 감지할 때 for 루프를 종료하게 됩니다.``

```go
package main
func main(){
   ch := make(chan string,2)
   ch <- "msg1"
   ch <- "msg2"
   close(ch)
   //방법 1
   for {
      if i, success := <-ch; success {
         println(i)
      } else {
         break
      }
   }

   // 방법2
   for i := range ch{
      println(i)
   }
}
```

## 채널의 select문
- Go의 select문은 복수 채널들을 기다리면서 준비된 (데이터를 보내온) 채널을 실행하는 기능을 제공한다. 즉, ``select문은 여러 개의 case문에서 각각 다른 채널을 기다리다가 준비가 된 채널 case를 실행하는 것이다.`` __select문은 case채널들이 준비되지 않으면 계속 대기__ 하게 되고, 가장 먼저 도착한 채널의 case를 실행한다. ``만약 복수 채널에 신호가 오면, Go 런타임이 랜덤하게 그 중 한개를 선택`` 한다. 하지만, __select문에 default문이 있으면, case문 채널이 준비되지 않더라도 계속대기하지 않고 바로 default문을 실행__ 한다.

- 아래 예제는 for 루프 안에 select 문을 쓰면서 두 개의 goroutine이 모두 실행되기를 기다리고 있습니다. 첫 번째 ``run1()``이 1초간 실행되고 done1 채널로부터 수신하여 해당 case를 실행하고, 다시 for 루프를 돌게 됩니다. for루프를 다시 돌면서 다시 select문이 실행되는데, 다음 ``run2()``가 2초 후에 실행되고 done2 채널로부터 수신하여 해당 case를 실행하게 됩니다. done2 채널 case문에 break EXIT 이 있는데, 이 문장으로 인해 for 루프를 빠져나와 EXIT 레이블로 이동하게 됩니다. __Go의 "break 레이블" 문은 C/C# 등의 언어에서의 goto문과 다른데, Go 에서는 해당 레이블로 이동한 후 자신이 빠져나온 루프 다음 문장을 실행하게 됩니다.__ 따라서, 여기서는 for 루프 다음 즉 ``main()`` 함수의 끝에 다다르게 됩니다.

```go
package main
import "time"
func main(){
   done1 := make(chan bool)
   done2 := make(chan bool)
   go run1(done1)
   go run2(done2)
   
EXIT:
   for {
      select {
         case <-done1:
            println("run1 이(가) 완료되었습니다")

         case <-done2:
            println("run2 이(가) 완료되었습니다")
            break EXIT
      }
   }
}
func run1(done chan bool){
   time.Sleep(1 * time.Second)
   done <- true
}
func run2(done chan bool){
   time.Sleep(2 * time.Second)
   done <- true
}
```