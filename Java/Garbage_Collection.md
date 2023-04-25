# 가비지 컬렉션(Garbage Collection)

## 메모리 누수 (Memory Leak) 

어디서도 참조되지 않는데도 메모리를 계속 할당받은 채로 소유하고 있는 경우를 말합니다.

## 가비지 (Garbage), 사용되지 않는 객체(Unreachable)

JVM의 가비지 컬렉션이 사용하지 않는 변수를 제거해줍니다.
더 이상 사용하지 않는 공간을 __'가비지(Garbage)'__ 라고 할 수 있습니다. 

```java
User user = new User("팔슨");

user = new User("게도");
```

위 코드에서 두 개의 객체가 생성됩니다. 

처음 user의 팔슨 객체가 생성되었을 땐 가비지가 없지만, user가 게도를 생성하면서 유저 객체는 팔슨을 더 이상 참조하지 않게 되고 바로 이때 "팔슨" 객체는 어디서도 참조되지 않는 __Unreachable 상태__ 가 되며 가비지로 인식되어 가비지 컬렉션에 의해 메모리 공간을 회수 당합니다.

## Minor GC와 Major GC

객체는 대부분 일회성이며, 메모리에 오랫동안 남아있는 경우는 드뭅니다. 그렇기에 객체의 생존 기간에 따른 물리적인 Heap 영역을 나누고, 그 영역은 각각 Young 영역과 Old 영역으로 설계되었습니다.

### Young 영역 (Young Generationm, Minor GC)
- 새롭게 생성된 객체가 메모리를 할당받는 영역
- 대부분의 객체는 금방 Unreachable 상태가 되기 때문에, 많은 객체가 Young 영역에 생성되었다가 사라집니다.

### Old 영역 (Old Generation, Full GC)
- Young 영역에서 Reachable 상태(메모리를 할당 받은 상태)를 유지하여 살아남은 객체가 복사되는 영역입니다.
- Young 영역보다 메모리가 크게 할당됩니다.
- Old 영역이 Young 영역보다 많은 메모리를 할당 받는 이유는 Young 영역의 객체들은 수명이 짧아 큰 공간을 필요로 하지 않고 큰 객체들은 Young 영역이 아니라 바로 Old 영역에 할당되기 때문입니다.

## 가비지 컬렉션의 동작방식

### Stop the World

가비지 컬렉션이 동작할 때는 따로 스레드를 두고 동작하는 것이 아닌, 실행되고 있는 모든 스레드를 중단하고 가비지 컬렉션을 실행합니다. GC의 성능 개선을 위해 __튜닝__ 을 한다고 하면이 중단 시간을 줄이는 것을 의미합니다.

### Mark and Sweep

- Mark : 사용되는 메모리와 사용되지 않는 메모리를 식별하는 작업
- Sweep : Mark 단계에서 사용되지 않음으로 식별된 메모리를 해제하는 작업

### 가비지 컬렉션의 구조

- Eden : 새로 생성된 객체가 할당되는 영역
- Survivor : 최소 1번의 Mark에서 살아남은 객체가 존재하는 영역이 2개 존재함

1. 객체가 생성되고 Eden 영역에 할당된다.
2. 객체가 계속 생성되고 Eden 영역이 꽉차게 되고 Minor GC가 실행된다.
    1. Eden에서 사용되지 않는 객체의 메모리가 해제된다.
    2. Eden에서 살아남은 객체는 Survivor으로 이동된다.
3. 1~2의 과정이 반복되다 Survivor 영역 또한 가득차게 되면 Survivor 영역의 살아남은 객체를 다른 Survivor 영역으로 이동시킨다.(1개의 Survivor 영역은 반드시 비어있는 상태입니다.)
4. 위 과정을 반복하다 Survivor 영역 또한 가득차게 되면 객체들을 Old 영역으로 이동(Promotion)

## Reachability
> Java GC는 객체가 사용되고 있는 지를 분류하기 위해 'Reachability'란 개념을 사용한다.

Reachability는 객체가 유효한 참조를 하고 있을 경우 'reachable', 아닐 경우 'unreachable' 로 구별하고 unreachable 객체를 가비지로 간주해 GC를 수행합니다.

유효한 참조 또한 파악하기 위해 'root set' 이라는 항상 유효한 최초의 참조라는 것을 reachable의 기준으로 둔다.


*출처 : Naver D2*
![reachablilty.png](..%2Fimages%2Freachablilty.png)
위에서 보듯이, root set으로부터 시작한 참조 사슬에 속한 객체들은 reachable 객체이고, 이와 무관한 객체들이 unreachable 객체로 GC 대상입니다. 오른쪽 아래 객체처럼 reacahble 객체를 참조하고 있을 지라도 본인이 참조받지 않는다면 unreachable 객체입니다.

물론 위의 개념은 가장 GC가 처리할 객체를 분류하는 가장 기본적인 내용이며 더 자세한 내용은 strongly reachable, softly reachable, weakly reachable, phantomly reachable를 검색해보시면 알 수 있으실 것입니다.