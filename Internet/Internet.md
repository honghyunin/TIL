# 인터넷 

__TCP/IP 통신 프로토콜__ 을 이용하여 서로 정보를 주고 받도록 하는 컴퓨터 네트워크를 말한다.  

<br>

# 인터넷 작동 원리

[인터넷 작동 원리 설명 글](https://developer.mozilla.org/ko/docs/Learn/Common_questions/How_does_the_Internet_work)  <br>
[인터넷 작동 원리 영상 ](https://www.youtube.com/watch?v=o5yBl59wRbY&ab_channel=%EA%B3%B5%ED%95%99%EC%BD%94%EB%84%88)

<br>


# 호스팅

서버 컴퓨터나, 서버 컴의 일정 공간을 이용할 수 있도록 임대해주는 서비스를 말한다.  

<br>

## 프로토콜 

인터넷을 원활하게 연결 등을 위한 방법을 칭한다.

## HTTP 

HTML 문서와 같은 리소스들을 가져올 수 있도록 하는 프로토콜이다
## 웹 호스팅

<br>
여러 대의 웹사이트를 한 서버에 운영하는 방식이다. 
<br>

_웹 호스팅 서비스_
 __무료__
  - Sentora
  - VestaCP

<br>

# 도메인

__URL : Uniform Resource Locator__

 - 사이트를 기억하기 쉽게 만들어주는 이름이자 특정 컴퓨터를 가리키는 주소이다.

 <br>

## DNS 

우리가 인터넷을 편리하게 쓰게 해주는 기술로 영문/한글 IP 네트워크에서 찾아갈 수 있는 IP로 변환해준다.

- DNS는 도메인 이름과 IP주소를 서로 변환하는 역할을 한다.

<br>

### DNS 동작

1. PC 브라우저에서 www.naver.com 을 입력한다. 그러면 pc는 미리 설정되어 있는 DNS(Local DNS, 예시는 203.248.252.2) 에게 "www.naver.com 이라는 hostname" 에 대한 IP 주소를 요청한다.

2. ``Local DNS`` 에는 "www.naver.com 의 IP 주소" 가 있을 수도 없을 수도 있다. 만약 있다면 Local DNS가 바로 PC에 IP 주소를 주고 끝난다. 하지만 본 설명에서는 __Local DNS에 "www.naver.com의 IP 주소"가 없다고 가정__ 한다.

3. Local DNS는 이제 "www.naver.com 의 IP 주소"를 찾아내기 위해 __다른 DNS 서버들과 통신(DNS 메시지)__ 을 __시작__ 한다.

<br>

### 브라우저

사용자가 보고자 하는 페이지를 서버에 요청하고 서버로부터 받은 응답(HTML, CSS, JavaScript 등)을 브라우저에 표시하는 것이다.

### 렌더링 엔진

브라우저에서 HTML, CSS를 띄우기 위해 처리해주는 것이다.

### 라우팅 Routing

유저가 패스를 통해 접속하였을 때 패스마다 응답을 해주는 것이다.

<br>

### 미들웨어

  데이터를 주고 받을 수 있도록 중간에서 매개 역할을 하는 소프트웨어이다.
  또한 미들웨어는 여러 종류가 있으며 다양한 방식으로 사용된다.

<br>

  ### URL 리다이렉션

  특정 웹사이트로 이동시키는 방법으로, URL을 단축시키거나 죽은 링크를 방지하기 위함 등의 목적으로 사용된다.