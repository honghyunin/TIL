# UserDetails

Spring Security에서 사용자의 정보를 담는 인터페이스는 UserDetails 이다. 우리가 이 인터페이스를 구현하게 되면 Spring Security에서 구현한 클래스를 사용자 정보로 인식하고 인증 작업을 한다. 쉽게 말하면 UserDetails 인터페이스는 VO 역할을 한다고 보면 된다. 그래서 우리는 사용자의 정보를 모두 담아두는 클래스로 구현할 것이다

아래 메소드들은 UserDetails를 구현하게 되면 오버라이드되는 메소드들이다. 

|메소드 명|리턴타입|설명|기본값|
|---------|---------|----|------|
|getAuthorities()||Collection<? extends GrantedAuthority|계정이 갖고 있는 권한 목록을 리턴한다|
|getPassword()|String|계정의 비밀번호를 리턴한다.|
getUsername()|String|계정의 이름을 리턴한다.|
isAccountNonExpired()|boolean|계정이 만료되지 않았는 지 리턴한다. |(true : 만료 안됨)
isAccountNonLocked()|boolean|계정이 잠겨있지 않았는 지 리턴한다. | (true : 잠기지 않음)
isCredentialNonExpired()|boolean|비밀번호가 만료되지 않았는 지 리턴한다. (true: 만료안됨)
isEnabled()|boolean|계정이 활성화(사용가능)인 지 리턴한다. (true: 활성화 됨)

getUsername()

- username은 계정의 고유한 값인데 로그인 용 서버를 제작한다고 했을 때 DB에서 User Table에 PK 값을 넘긴다.

# UserDetailService

Spring Security에서 유저의 정보를 가져오는 역할을 한다.

> 유저의 정보를 불러오기 위해서 구현해야하는 인터페이스로 기본 오버라이드 메서드는 아래와 같다

|메소드 명|리턴타입|설명|
|---|----|----|
loadUserByUsername|UserDetails|유저의 정보를 불러와서 UserDetails로 리턴|


🙆‍♂️ 참고 🙇‍♂️

https://to-dy.tistory.com/86