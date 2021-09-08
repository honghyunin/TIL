# Spring MVC 구조의 처리 과정

![mvc](/images/Spring_MVC.png)

|구성 요소|설명|
|-|-|
__DispatcherServlcet__ | 애플리케이션으로 들어오는 모든 Request를 받는 부분
__HandlerMapping__| 클라이언트의 요청 URL을 어떤 컨트롤러가 처리할지 결정
__Controller__ | 클라이언트의 요청을 처리한 뒤, 결과를 DispatcherServlet에게 리턴
__ModelAndView__  | 컨트롤러가 처리한 결과 정보 및 뷰 선택에 필요한 정보를 담음
__ViewResolver__ | 컨트롤러의 처리 결과를 생성할 뷰를 결정
__View__ | 컨트롤러의 처리 결과 화면을 생성, JSP 또는 Velocity 템플릿 파일 등을 뷰로 사용

# Spring MVC 동작 과정

1. 사용자가 URL을 통해서 Request를 전송한다.
2. DispatcherServlet은 Request를 처리하기 위한 Controller를 HandlerMapping 빈 객체에게 검색 요청을 한다.
3. HandlerMapping은 Client의 URL을 이용해서 이를 처리할 Controller 빈 객체를 DispathcerServlet에게 return 한다.
4. DispathcerServlet은 Controller 객체를 처리할 수 있는 HandlerAdatper 빈에게 요청 처리를 위임한다.
- @Controller, Controller Interface, HttpRequestHandler Interface를 동일한 방식으로 처리하기 위해 HandlerAdapter 빈이 중간에 사용된다.
5. HandlerAdapter는 Controller에게 알맞은 method를 호출한다.
6. Controller는 비즈니스 로직을 수행 한 후 처리 결과를 HandlerAdapter에게 return 한다.
7. HandlerAdapter는 DispatcherServlet에게 Controller의 실행 결과를 ModelAndView객체로 변환 하여 return 한다.
8. DispatcherServlet은 결과를 보여줄 View를 검색하기 위해 ViewResolver 빈 객체에게 ModelAndView안의 해당 view를 검색 요청한다.
9. ViewResolver는 ModelAndView안의 View 이름에 해당하는 View객체를 찾거나 생성해서 return 한다.
10. DispatcherServlet은 ViewResolver가 return한 View객체에게 request result 생성을 요청한다
