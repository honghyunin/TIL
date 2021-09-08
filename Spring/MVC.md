# MVC

> Model View Controller

## Model

: `Model`은 어플리케이션이 **"무엇"** 을 할 것인지를 정의합니다. __내부 비지니스 로직을 처리하기 위한 역할을 할 것입니다.__

- 애플리케이션의 상태(data)를 나타냅니다.
- 일반적으로 POJO로 구성됩니다.
- Java Beans

## Controller

: `Controller`는 모델이 **"어떻게"** 처리할지를 알려주는 역할을 할 것이고, 모바일에서는 **화면의 로직처리** 부분입니다. 화면에서 사용자의 요청을 받아서 처리하는 부분이 구현하게 되며, 요청 내용을 분석해서 Model과 View에 업데이트 요청을 하게 됩니다.

- View와 Model 사이의 인터페이스 역할
- Model/View 에 대한 사용자 입력 및 요청을 수신하여 그에 따라 적절한 결과를 Model에 담아 View에 전달합니다.
- Controller -> Service -> Dao -> DB
- Servlet


## View

: `View`는 화면에 **"무엇"** 인가를 **"보여주기 위한 역할"** 을 합니다. 컨트롤러 하위에 종속되어, 모델이나 컨트롤러가 보여주려고 하는 모든 필요한 것들을 보여줄 것입니다.

- **최종 사용자** 에게 "무엇"을 화면으로 보여줍니다

- 디스플레이 데이터 또는 프레젠테이션
- Model Data의 렌더링을 담당하며, HTML output을 생성합니다.
- JSP, Thymeleaf, Groovy, Freemarker 등 여러 Template Engine이 있습니다.
그리고 Controller는 Model과 View가 각각 무엇을 해야 할 지를 알고 있고, 통제합니다. 비지니스 로직을 처리하는 Model과 완전히 UI에 의존적인 View가 서로 직접 이야기를 할 수 없게 합니다.

# MVC의 한계

MVC에서 View는 Controller에 연결되어 화면을 구성하는 단위요소이므로 다수의 View들을 가질 수 있습니다. 그리고 Model은 COntroller를 통해서 View와 연결되어지지만, 이렇게 Controller를 통해서 하나의 View에 연결될 수 있는 Model도 여러개가 될 수 있습니다.
