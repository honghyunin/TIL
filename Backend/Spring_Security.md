# Spring Security란?

<hr>

Spring Security는 Spring 기반의 **애플리케이션의 보안(인증과 권한)을 담당하는 스프링 하위 프레임워크**이다.

Spring Security는 **'인증'과 '권한'에 대한 부분을 Filter 흐름에 따라 처리**하고 있다.  Filter는 spring MVC와 분리되어 관리 및 동작한다. 

## Spring Securit의 구조

#### 인증 관련 Architecture

![Architecture](/images/architecture.png)

### [인증과 인가]

- 인증(Authentication) : 해당 사용자가 본인이 맞는 지를 확인하는 절차
- 인가(Authorization) : 인증된 사용자가 요청한 자원에 접근 가능한 지를 결정하는 절차
- Principal(접근 주체) : 보호된 대상에 접근하는 유저
- Credential(비밀번호) : 대상에 접근하는 유저의 비밀번호

Spring Security는 기본적으로 인증 절차를 거친 후에 인가 절차를 진행하게 되며, 인가 과정에서 해당 리소스에 대한 접근 권한이 있는 지를 확인하게 된다.

Spring Security에서는 이러한 인증과 인가를 위해 `Principal`을 아이디로, `Credential`을 비밀번호로 사용하는 `Credential 기반의 인증 방식`을 사용한다.

