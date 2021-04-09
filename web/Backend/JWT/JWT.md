# JWT (Json Web Token)

## 💰 JWT란?
- JWT는 클라이언트와 서버, 서비스와 서비스 사이 통신 시 권한 인가(Authorization)를 위해 사용되는 토큰입니다. 
- URL에 대해 안전한 문자열로 구성되어 있기 떄문에 HTTP 어디든 (URL, Header) 위치할 수 있습니다.

## 🎲 JWT 토큰 구성

![JWT 구성](/images/jwt구성.png)

- JWT는 세 부분으로 나눠지며, 각 부분은 점으로 구분하여 위 사진과 같이 표현됩니다.


1. Header는 토큰의 타입과 해시 암호화 알고리즘으로 구성되있습니다. 
    - 첫 번째는 토큰의 유형을 나타내고, 두 번째는 해쉬 알고리즘을 나타내는 부분입니다.
2. Payload는 토큰에 담을 클레임(Claim) 정보를 포함하고 있습니다. 이 클레임은 name / value 로 한 쌍을 이뤄져있습니다. 또한 토큰에는 여러개의 클레임 들을 넣을 수 있습니다. 클레임의 정보는 등록된 (registered) 클레임, 공개 (public) 클레임, 비공개 (private) 클레임으로 세 종류가 있습니다.
    - 토큰의 페이로드에는 토큰에서 사용할 정보의 조각들인 클레임(Claim)이 담겨 있습니다. 클레임은 3가지로 나뉘며, JSON(Key/Value) 형태로 다수의 정보를 넣을 수 있습니다.

    2.1 등록된 클레임(Registered Claim)

    등록된 클레임은 토큰 정보를 표현하기 위해 이미 정해진 종류의 데이터들로, 모두 선택적으로 작성이 가능하여 사용할 것을 권장합니다. 또한 JWT를 간결하게 하기 위해서는 key는 모두 길이 3의 문자열로 표시합니다. 


    ```
    iss: 토큰 발급자(issuer)

    sub: 토큰 제목(subject)

    aud: 토큰 대상자(audience)

    exp: 토큰 만료 시간(expiration), NumericDate 형식으로 되어 있어야 함 ex) 1480849147370

    nbf: 토큰 활성 날짜(not before), 이 날이 지나기 전의 토큰은 활성화되지 않음

    iat: 토큰 발급 시간(issued at), 토큰 발급 이후의 경과 시간을 알 수 있음

    jti: JWT 토큰 식별자(JWT ID), 중복 방지를 위해 사용하며, 일회용 토큰(Access Token) 등에 사용
    ```

    2.2 공개 클레임(Public CLaim)

    공개 클레임은 사용자 정의 클레임으로, 공개용 정보를 위해 사용됩니다. 충돌 방지를 위해 URL 포멧을 사용합니다.

    ```javaScript
    {"https://hyunin.co.kr":true}
    ```

    2.3 비공개 클레임(Private Claim)
    비공개 클레임은 사용자 정의 클레임으로, 서버와 클라이언트 사이에 임의로 지정한 정보를 저장합니다. 

    ```javaScript
    {"token_type":access}
    ```

    3. Signature는 secret key를 포함하여 암호화되어 있습니다.
        - 서명(Signatuer)은 토큰을 인코딩하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드이다. 위에서 만든 헤더(Header)와 페이로드(Payload)의 값을 각각 BASE64로 인코딩하고, 인코딩한 값을 비밀 키를 이용해 헤더에서 정의한 알고리즘으로 해싱을 하고 이 값을 다시 BASE64로 인코딩하여 생성한다.

# JWT 작동과정

1. 사용자가 ID와 PASSWORD를 입력하여 로그인 시도합니다.
2. 서버는 요청을 확인하고 secret key를 통해 Acess token을 발급합니다.
3. JWT 토큰을 클라이언트에 전달합니다.
4. 클라이언트에서 API를 요청할 때 클라이언트가 _Authorization header_(인증 토큰을 서버로 보낼 때 사용하는 헤더)에 Access token을 담아서 보냅니다.
5. 서버는 JWT Signature를 체크하고 Payload로부터 사용자 정보를 확인해 데이터를 반환합니다.
6. 클라이언트의 로그인 정보를 서버 메모리에 저장하지 않기 때문에 토큰기반 인증 메커니즘을 제공합니다.
인증이 필요한 경로에 접근할 때 서버 측은 Authorization 헤더에 유효한 JWT 또는 존재하는 지 확인합니다.
JWT에는 필요한 모든 정보를 토큰에 포함하기 때문에 DB와 같은 서버와의 커뮤니케이션 오버 헤드를 최소화할 수 있습니다.
Cross-Origin Resource Sharing(서로 다른 origin 간 HTTP Req가 가능하도록 해주는 표준입니다.)는 쿠키를 사용하지 않기 때문에 JWT를 채용 한 인증 메커니즘은 두 도메인에서 API를 제공하더라도 문제가 발생하지 않습니다.
_처음 사용자를 등록할 때 Access token과 Refres token이 모두 발급되어야 합니다._


