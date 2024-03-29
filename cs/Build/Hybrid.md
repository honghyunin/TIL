# ⚙️ Hybrid Type

- 컴파일 방식과 인터프리트 방식을 혼합한 방법입니다.

- 흔히 __'바이트 코드 언어(Byte Code Language)'__ 라고 부릅니다. 대표적인 언어로는 Java(자바) 가 있습니다.

<hr>

# 📃 번역 과정

- 고급 언어로 작성된 소스 코드를 바이트 코드(ByteCode)로 변환합니다. 바이트 코드는 중간 언어라고 생각하면 됩니다. 그리고 VM(Virtual Machine : 가상머신 프로그램) 이라는 프로그램에 의해 바이트코드를 기계어로 바꿔줍니다.

- 하이브리드 타입은 VM 이라는 가상머신 프로그램에서 소스코드를 실행한다고 보시면 됩니다. 즉, 각 플랫폼에 맞는 VM들이 있다면 우리는 같은 소스코드를 어느 플랫폼에서든지 동일한 결과를 얻어낼 수 있다는 것입니다.

<hr>


![ByteCode](../images/ByteCode.png)


<hr>

- __바이트 코드(Byte Code)__ 는 가상머신이 이해할 수 있는 __중간언어(Intermediate Language)__ 라고 보시면 됩니다. 예를 들어 JAVA를 컴파일 하면 .class 파일이 생성될 겁니다. _바이트코드는 기계어는 아니지만 어셈블리어처럼 '기계에 조금 더 가까운 언어'로 되어있죠_

- 컴파일언어의 목적파일과 차이가 있다면 컴파일 언어안에서는 하드웨어에 의해 처리되는 기계어로 되어있었다면, 바이트 코드 파일의 경우 하드웨어가 직접 처리하는 것이 아닌 소프트웨어(가상 머신)에 의해 처리된다는 것입니다. 역으로 생각하면 바이트코드는 해당 가상머신 전용 기계어라고 보면 됩니다.

- VM은 가상 컴퓨터입니다. 하나의 컴퓨터 환경을 구현한 것이죠.
    - 바이트 코드는 이 가상머신이 이해할 수 있는 코드로 되어있습니다. 그리고 그 가상머신 안에는 인터프리터 같은 해석기가 있어 이들이 바이트코드를 해석하여 각 OS에 맞게 명령어를 해석하고 작동하는 하나의 프로그램이라고 보면 되죠.

<hr>

# 하이브리드의 장점

- 각 플랫폼에 지원하는 가상머신이 있다면 실행 가능하기 때문에 플랫폼에 독립적입니다.

# 하이브리드의 단점
- 컴파일 언어처럼 하드웨어를 직접 제어하는 작업은 불가능합니다.

<hr>

# 📙 정리

- `플랫폼에 독립적` 인 장점을 갖고있고,초기 컴파일 단계를 통해 바이트코드로 기계어에 더 가까운 언어로 번역을 한 번 해놓았기 때문에 속도도 기존 인터프리터 언어에 비해 더 빠르다는 장점 또한 갖고오게 되었죠.