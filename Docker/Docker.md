# [Docker] 도커란?

> Docker는 애플리케이션을 신속하게 구축, 테스트 및 배포할 수 있는 소프트웨어 플랫폼입니다

코딩을 해봤다면 개발 환경을 구성하는 일이 꽤나 어려운 일임을 느껴보셨을 것입니다 아무리 코딩을 열심히 해도 호환되지 않은 버전으로 했다면..
모두 다 갈아엎어야 하는 상황이 생길 수도 있습니다.

하지만 이 것을 해결해줄 수 있는 것이 바로 ``도커``입니다!


# 도커는 왜 사용할까?

도커는 특정 프로젝트를 진행하거나 프로그램을 실행시키기 위한 환경을 그대로 가져와 사용할 수 있습니다

### ?? 무슨 말이죠

다시 말해 우리가 몇 년동안 사용한 컴퓨터가 있다고 가정해봅시다
그런데 이 컴퓨터를 너무 오래 사용해 새로 컴퓨터를 구매하여 이 전에 쓰던 컴퓨터처럼 새로 셋팅을 해야하는데 어디서부터 어떻게해야할지 너무 막막하고 시간 낭비도 엄청날 것입니다

하지만 도커를 사용하면 이전 PC 환경 전부를 새로운 PC에 단 몇 개의 명령어 만으로 구성이 가능해집니다!!

# 도커의 기본개념

> __도커__ : 컨테이너를 사용하며 응용 프로그램을 더 쉽게 만들고 배포하고 실행할 수 있도록 설계된 도구이며 컨테이너 기반의 오픈 소스 가상화 플랫폼이며 생태계입니다.

``도커``에서 ``컨테이너``란 여러분들이 자주 접하는 컨테이너와 비슷합니다
 
 실제 컨테이너는 물건들을 다른 나라에 수출하거나 수입해올 때 용됩니다 컨테이너를 사용하면 물품 분류에도 용이하고 운반이 더욱 편리해집니다

 도커에서의 컨테이너는 안에 다양한 프로그램, 실행 환경을 컨테이너로 추상화하고 동일한 인터페이스를 제공하여 프로그램의 배포 및 관리를 용이하게 해줍니다.

 ## 도커 이미지와 도커 컨테이너

도커 컨테이너의 정의입니다

 > 도커 컨테이너 : 코드와 모든 종속성을 패키지화하여 응용 프로그램이 한 컴퓨터 환경에서 다른 컴퓨터 환경으로 빠르고 안정적으로 실행되도록 하는 소프트웨어 표준 단위입니다.

 다시 말해, 간단하고 편리하게 프로그램을 실행시켜주는 것이죠.

## 도커 이미지

컨테이너 이미지 정의입니다
> 코드, 런타임, 시스템 도구, 시스템 라이브러리 및 설정과 같은 응용 프로그램을 실행하는데 필요한 모든 것을 포함하는 가볍고 독립적이며 실행 가능한 소프트웨어 패키지입니다.


이미지가 프로그램을 실행할 수 있는 모든 것을 갖추고 있고 컨테이너는 이를 실행할 수 있도록 해주는 것이라고 이해하면 좋ㅅ브니다