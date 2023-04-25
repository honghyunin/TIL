# Spring Security란?


> Spring Security는 Spring 기반의 **애플리케이션의 보안(인증과 권한)을 담당하는 스프링 하위 프레임워크**이다.
Spring Security는 **'인증'과 '권한'에 대한 부분을 Filter 흐름에 따라 처리**하고 있다.  Filter는 spring MVC와 분리되어 관리 및 동작한다. 

## Spring Securit의 구조

#### 인증 관련 Architecture

![architecture.png](..%2Fimages%2Farchitecture.png)

### [인증과 인가]

- 인증(Authentication) : 사용자가 서비스를 사용할 자격이 있는 지 확인하는 과정
    - 인증에 성공하면 사용자에게 설정된 권한을 할당
    - ex) 로그인

- 인가(Authorization) : 접근하는 사용자가 해당 로직 및 url에 접근할 권한을 가지고 있는 지 확인하는 과정
    - 웹 요청, url, 도메인 인스턴스에 대한 접근을 관리
    - 만약 접근 한 사용자가 권한이 없거나 낮으면 (ex 관리자 요청을 일반 유저가 요청한 경우) 요청을 거부한다.

- Principal(접근 주체) : 보호된 대상에 접근하는 유저

- Credential(비밀번호) : 대상에 접근하는 유저의 비밀번호

- Authentication 객체 : Spring Security에서 한 유저의 인증 정보를 가지고 있는 객체, 사용자가 인증 과정을 성공적으로 마치면, Spring Security는 사용자의 정보 및 인증 성공여부를 가지고 Authentication 객체를 생성한 후 보관한다.

- SecurityContextHolder : Authentication 객체를 보관하는 곳, 애플리케이션 어디에서든지 접근할 수 있음

- UserDetails : 일반 서비스의 사용자 객체를 Spring Security에서 사용하는 사용자 객체와 호환해주는 어댑터

- UserDetailsService - Spring Security에서 로그인할 때 전달된 정보를 기반으로 DB에서 유저를 가져오는 책임을 가지는 인터페이스

- GrantedAuthority : 사용자에게 주어진 애플리케이션 사용 권한 객체

PasswordEncoder : DB에 사용자의 정보 저장 시 비밀번호를 암호화 해주거나, 인증 시 입력 된 비밀번호와 저장 된 비밀번호를 mathcing 해주는 객체.
Spring Security는 기본적으로 인증 절차를 거친 후에 인가 절차를 진행하게 되며, 인가 과정에서 해당 리소스에 대한 접근 권한이 있는 지를 확인하게 됩니다.

Spring Security에서는 이러한 인증과 인가를 위해 `Principal`을 아이디로, `Credential`을 비밀번호로 사용하는 `Credential 기반의 인증 방식`을 사용합니다.

# Securtiy의 Filters

- SecurityContextPersistenceFilter : SecurtiyContextRepository에서 SecurityContext를 가져오거나 저장하는 역할을 한다.
- LogoutFilter : 설정된 로그아웃 URL로 오는 요청을 감시하며, 해당 유저를 로그아웃 처리
3. UsernamePasswordAuthenticationFilter : 아이디와 비밀번호를 사용하는 form 기반 인증, 설정된 로그인 URL로 오는 요청을 감시하며, 유저 인증 처리
    1. AuthenticationManager를 통한 인증 실행
    2. 인증 성공 시, 얻은 Authentication 객체를 SecurityContext에 저장 후 AuthenticationSuccessHandler 실행
    3. 인증 실패 시, AuthenticationFailureHandler 실행
4. DefaultLoginPageGeneratingFilter : 인증을 위한 로그인 폼 URL을 감시한다.
5. BasicAuthenticationFilter : HTTP 기본 인증 헤더를 감시하여 처리한다.
6. RequestCacheAwareFilter : 로그인 성공 후, 원래 요청 정보를 재구성하기 위해 사용된다.
7. SecurityContextHolderAwareRequestFilter : HttpServletRequestWrapper를 상속한
SecurityContextHolderAwareWapper 클래스로 HttpServletRequest 정보를 감싼다.
SecurityContextHolderAwareWapper 클래스는 필터 체인상의 다음 필터들에게 부가 정보를 제공한다.

# 로그인 인증 과정

1. 유저가 입력한 아이디 비밀번호를 Spring Security가 사용하는 유저의 객체로 변환 시킴(UserDetails 이용)
2. 유저가 입력한 정보를 기반으로 DB에서 사용자 정볼르 가져옴 (UserDetailsService 인터페이스의 역할)
3. 유저가 입력한 정보와 DB에서 가져온 사용자 정보를 기반으로 인증 진행 (AuthenticationManager 인터페이스의 authenticate() 메소드)
4. 인증에 성공했다면 유저에게 설정된 권한을 부여함

# 인증 관련 세부 내용

``AuthenticationManager``
- authentication 메소드를 가지고 있는 인터페이스로 Spring Security에서 인증을 담당하는 메소드

``ProdvidManager``
- Spring Security에서 AuthenticationManager의 기본 구현체
- 이 클래스는 자신이 가지고 있는 여러 AuthenticationProvider들에게 인증 처리를 위임함

``AuthenticationProdvider``
- 실질적으로 인증을 처리하는 클래스(authentication 메소드를 구현한 클래스)
- UserDetails와 UserDetailsService 그리고 PasswordEncoder를 이용해서 인증을 처리
- ProviderManager는 여러개의 AuthenticationProdvider를 가질 수 있음
- 여러개의 AuthenticationProvider를 가지고 있는 경우 각 순서대로 인증을 진행하거나, skip 함.
- 만약 모든 AuthenticationProvider가 null를 반환(인증을 skip했다는 것)하면 ProviderNotFoundException을 반환함
- Spring Security에서 구현한 여러 AuthenticationProvider 구현체들이 있음.
DaoAuthenticationProvider, LdapAuthenticationProvider : form 기반 로그인이나, HTTP Bagic authentication 인증을 구현한 구현체

``DaoAuthenticationProvider``
- 유저가 입력한 username, password를 DB에서 가져온 유저 정보와 비교하여 인증을 처리하는 구현체

- password를 비교하기 위해서 PasswordEncoder를 설정
- DB에서 유저 정보를 가져오기 위해 UserDetailsService를 설정

``UserDetailsService``
- 사용자가 입력한 username을 기반으로 저장된 유저 정보를 가져와서 UserDetails 객체로 변환하여 돌려주는 메소드
- UserDetails loadUserByUsername(String username) throws UsernameNotFoundException; 메소드 하나를 가지고 있는 인터페이스
- Spring Security에서 관련 구현체로 In-Memory Authentication, JdbcDaoImpl이 있음

``In-Memory Authentication``
- 애플리케이션의 메모리 안에 유저 정보를 저장해두고, 인증 요청이 있을 때 이 정보들 중에서 입력된 정보와 일치하는 유저를 반환해주는 구현체
- 프로토타입용으로만 사용하는 것이 좋음(절대 실무에서 사용하면 안됨)

``JdbcDaoImpl``
- DB에서 쉽게 입력된 사용자 정보를 가져올 수 있음.
- 하지만 ORM을 사용한다면 직접 UserDetailsService 인터페이스를 구현하여 사용하는 것이 좋음

``UserDetails``
- Spring Security에서는 사용자 객체가 필요하지만, 모든 서비스 마다 사용자 정의가 다르기 때문에 서비스와 Spring Security의 사용자 객체를 호환해주는 어댑터인 UserDetails가 필요
- Spring Security를 사용하는 애플리케이션에서는 이 인터페이스를 구현해야 함.

``PasswordEncoder``
- 사용자가 입력한 password를 암호화해줌