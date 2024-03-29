# 스프링 컨테이너 종류

스프링 프레임워크는 스프링의 빈을 생성하고 관리하는 컨테이너를 가지고 있다. 이를 통해서 스프링의 주개념인 IOC 나 AOP에 대해서 관리하고 합니다.

# ApplicationContext

- 스프링 애플리케이션 전반에 걸쳐 모든 구성요소의 제어 작업을 담당하는 **IoC 엔진**입니다.

- IoC 방식을 따라 만들어진 일종의 빈 팩토리이다. 빈 팩토리라고 말할 때는 빈을 생성하고 관계를 설정하는 IoC의 기본 기능에 초점을 맞춘 것이고, 애플리케이션 컨텍스트는 별도의 정보를 참고해서 **빈의 생성, 관계설정 등의 제어를 총괄**합니다.

또한 싱글톤을 저장하고 관리하는 __싱글톤 레지스트리__ 입니다. __스프링은 기본적으로 별다른 설정을 하지 않으면 내부에서 생성하는 빈 오브젝트를 모두 싱글톤으로 만듭니다.__


[책 읽는 개발자_테드님의 게시글](https://scshim.tistory.com/32)