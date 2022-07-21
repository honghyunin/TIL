# Servlet 이란?

- Servlet : 클라이언트의 요청을 응답해주는 자바프로그램

예시로 사용자가 로그인을 하기 위해 아이디와 비밀번호를 입력하고 로그인 버튼을 누릅니다.

그때 서버는 클라이언트의 아이디와 비밀번호를 확인하고, 다음 페이지를 띄워주어야 하는데 이러한 역할을 수행하는 것이 서블릿(Servlet)입니다. 그래서 서블릿은 자바로 구현 된 *CGI라고 흔히 말합니다.

- CGI(Common Gateway Interface)란?

```markdown
CGI는 클라이언트의 요청을 받아 처리해줄 로직을 담고 있는 애플리케이션 프로그램 사이의 인터페이스이다.
```

# [ Servlet 특징 ]

- 클라이언트의 요청에 대해 동적으로 작동하는 웹 어플리케이션 컴포넌트입니다
- html을 사용하여 요청에 응답합니다
- Java Thread를 이용하여 동작합니다
- MVC 패턴에서 Controller로 이용됩니다
- HTTP 프로토콜 서비스를 지원하는 javax.servlet.http.HttpServlet 클래스를 상속받습니다.
- UDP보다 처리 속도가 느립니다.
- HTML 변경 시 Servlet을 재컴파일해야 하는 단점이 있습니다.

# [ Servlet 동작 방식 ]

![Servlet](/images/Servlet.png)

1. 사용자(클라이언트)가 URL을 입력하면 HTTP Request가 Servlet Container로 전송합니다.
2. 요청을 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse 객체를 생성합니다.
3. web.xml을 기반으로 사용자가 요청한 URL이 어느 서블릿에 대한 요청인지 찾습니다.
4. 해당 서블릿에서 service 메소드를 호출한 후 클라이언트의 GET, POST 여부에 따라 doGet() 또는 doPost()를 호출합니다.
- doGet() or doPost() 메소드는 동적 페이지를 생성한 후 HttpServletResponse객체에 응답을 보냅니다.

  5. 응답이 끝나면 HttpServletRequest, HttpServletResponse 두 객체를 소멸시킵니다.


# Servlet Container(서블릿 컨테이너)

- 서블릿 컨테이너 : 서블릿을 관리해주는 컨테이너

- 서버에 서블릿을 만들었다고 해서 스스로 작동하는 것이 아니고 **서블릿을 관리해주는 것**이 필요한데, 그러한 역할을 하는 것이 바로 서블릿 컨테이너입니다. 예를 들어, 서블릿이 어떠한 역할을 수행하는 정의서라고 보면, 서블릿 컨테이너는 그 정의서를 보고 수행한다고 볼 수 있습니다. 서블릿 컨테이너는 **클라이언트의 요청(Requeset)를 받아주고 응답(Response)할 수 있게, 웹서버와 소켓으로 통신**하며 대표적인 예로 톰캣(Tomcat)이 있습니다. 톰캣은 실제로 웹 서버와 통신하여 JSP(Java Server Page) 와 Servlet이 작동하는 환경을 제공해줍니다.

# [Servlet Container 역할]

## 1. 웹서버와의 통신 지원

**서블릿 컨테이너는 서블릿과 웹서버가 손쉽게 통신할 수 있게 해줍니다.** 일반적으로 우리는 소켓을 만들고 listen, accept 등을 해야하지만 서블릿 컨테이너는 이러한 기능을 API로 제공하여 복잡한 과정을 생략할 수 있게 해줍니다. 그래서 개발자가 서블릿에 구현해야 할 비즈니스 로직에 대해서만 초점을 두게끔 도와줍니다.

## 2. 서블릿 생명주기(Life Cycle) 관리

**서블릿 컨테이너는 서블릿를 만들거나 제거**합니다. 서블릿 클래스를 로딩하여 인스턴스화하고, 초기화 메소드를 호출하고, 요청이 들어오면 적절한 서블릿 메소드를 호출합니다.

또한 서블릿이 생명을 다 한 순간에는 적절하게 Garbage Collection(가비지 컬렉션)을 진행하여 편의를 제공합니다.

## 3. 멀티쓰레드 지원 및 관리

**서블릿 컨테이너는 요청이 올 때 마다 새로운 자바 쓰레드를 하나 생성**하는데, HTTP 서비스 메소드를 실행하고 나면, 쓰레드는 자동으로 죽게됩니다. 원래는 쓰레드를 관리해야 하지만 서버가 다중 쓰레드를 생성 및 운영해줍니다.

## 4. 선언적인 보안 관리

서블릿 컨테이너를 사용하면 개발자는 보안에 관련된 내용을 서블릿 또는 자바 클래스에 구현해 놓지 않아도 됩니다. 일반적으로 보안관리는 XML 배포 서술자에다가 기록하므로, 보안에 대해 **수정할 일이 생겨도 자바 소스 코드를 수정하여 다시 컴파일 하지 않아도 보안관리가 가능**합니다.

## [ Servlet 생명주기 ]

![Container](/images/server_Container.png)

1. 요청이 오면, Servlet 클래스가 로딩되어 요청에 대한 **Servlet 객체가 생성**됩니다.(이때 컨테이너는 해당 서블릿이 **메모리에 있는 지 확인하고, 있을 경우 기존의 서블릿을 제거하고 init() 메소드를 호출하여 재생성한다**)
2. 서버는 init() **메소드**를 호출해서 **Servlet을 초기화** 합니다.
3. service() 메소드를 호출해서 Servlet이 **브라우저의 요청을 처리**하도록 합니다.
4. service() 메소드는 특정 **HTTP 요청(GET, POST등)을 처리**하는 메서드(doGet(), doPost() 등)를 호출합니다.
5. 서버는 destroy() 메소드를 호출하여 **Servlet을 제거**합니다.

톰캣은 Servlet을 다음과 같이 관리하고 있습니다.

- Servlet 객체를 생성하고 초기화하는 작업은 비용이 많은 작업이믈, 다음에 또 요청이 올 때를 대비하여 이미 생성된 **Servlet 객체는 메모리에 남겨둡니다.**
- 또 톰캣이 종료되기 전이나 reload 전에 모든 Servlet을 제거하게 됩니다.
- 이렇게 톰캣은 자원을 아끼면서 Servlet을 사용하고 있습니다.

# JSP (Java Server Page)

- JSP :  HTML에 java코드를 삽입하여 ``동적인 웹 페이지``를 만들 수 있는 기술이다.

JSP는 ``servlet의 단점을 보완`` 하고자 만든 서블릿 기반의 ``스크립트`` 기술이다. ``Servlet``만을 이용해서도 웹 프로그래밍이 가능하지만 ``인터페이스(View)``를 구현하기 위해 너무 많은 코드가 필요하여 Servlet을 작성하지 않고도 간편하게 웹 프로그래밍을 구현할 수 있게 만든 것이 JSP이다. ( JSP는 웹 컨테이너에 의해서 Servlet으로 다시 변환되어 실행된다.)

# [ JSP 동작 구조]

![JSP](/images/JSP_1.png)

1. JSP 페이지 요청이 들어온다
2. JSP파일에 대한 Servlet 객체가 메모리에 존재하는 지 우선 확인한다. Servlet이 있다면 재활용하여 Thread만을 생성하여 처리하고, Servlet이 없다면 3번으로 진행한다.
3. JSP Container(Tomcat)가 JSP 페이지를 찾아 JSP Container이 JSP페이지를 Servlet으로 변환한 후 컴파일하여 실행한다.
4. Servlet으로 변환된 JSP 페이지를 확인하면 html 코드들은 servlet의 코드로 변환된 것을 확인할 수 있다.
5. 실행결과를 Client에게 돌려준다. (JSP 코드 등은 서버에서 처리한 후 HTML 파일을 응답하므로 소스보기를 해도 JSP 코드는 보이지 않는다.)

# 참고

- [https://mangkyu.tistory.com/14](https://mangkyu.tistory.com/14)
- [https://victorydntmd.tistory.com/154](https://victorydntmd.tistory.com/154)
- [https://galid1.tistory.com/488](https://galid1.tistory.com/488)