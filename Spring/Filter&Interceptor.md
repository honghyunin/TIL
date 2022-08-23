# Filter

> 필터 : J2EE 표준 스펙 기능, 디스패처 서블릿에 요청이 전달되기 전/후에 부가작업을 처리할 수 있는 기능을 제공

디스패처 서블릿은 스프링의 가장 앞단에 존재하는 프론트 컨트롤러이므로, 필터는 스프링 범위 밖에서 처리가 됩니다.

스프링 컨테이너가 아닌 웹 컨테이너에 의해 관리가 되고(스프링 빈으로 등록은 된다), 디스패치 서블릿 전/후에 처리하는 것입니다.

## Filter method

 > Filter는 interface이므로 다음 세가지의 메소드를 구현해야 합니다.
 
- init 메소드
- doFilter 메소드
- destroy 메소드

### init method
필터 객체를 초기화하고 서비스에 추가하기 위한 메소드입니다.
초기화 한 이후의 요청은 doFilter를 통해 처리됩니다.

### doFilter method
메소드 매개변수에있는 FilterChain을 통해 다음 대상으로 요청을 전달합니다.
chain.doFilter() 전/후에 우리가 필요한 처리 과정을 넣어줌으로써 원하는 처리를 진행할 수 있습니다.

### destroy method
필터 객체를 서비스에서 제거하고 사용하는 자원을 반환하기 위한 메소드입니다. 웹 컨테이너에 의해 한 번 호출되며 이후에는 doFilter에 의해 처리되지 않습니다.

![filter](/images/filter.png)

### 인터셉터
Spring이 제공하는 기술로써, 디스패처 서블릿이 컨트롤러를 호출하기 전과 후에 요청과 응답을 참조하거나 가공할 수 있는 기능을 제공합니다.

인터셉터는 스프링 컨텍스트에서 동작하여 필터를 거쳐 프론트 컨트롤러인 디스패처 서블릿이 요청을 받은 이후에 동작하게 됩니다.
[[Drawing 2022-08-23 15.51.35.excalidraw]]

## Interceptor method
> Interceptor는 interface이므로 다음 세가지의 메소드를 구현해야 합니다.

- preHandle 메소드
- postHandle 메소드
- afterCompletion 메소드

### preHandle method
preHandle method는 컨트롤러가 호출되기 전에 실행되어 전처리 작업이나 요청 정보를 가공, 추가하는 경우에 사용할 수 있습니다.

preHandle의 파라미터 중 handler은 핸들러 매핑이 찾은 HandlerMethod 라는 새로운 타입의 객체로써 @RequestMapping이 붙은 메소드의  정보를 추상화한 객체입니다.

preHandle의 반환 타입은 boolean인데, 반환 값이 true이면 다음 단계로 진행 되지만, false라면 작업을 중단합니다(다음 인터셉터 또는 컨트롤러).

### postHandle method
컨트롤러 호출 후 실행되어 후처리 작업이 있을 때 사용합니다.

### afterCompletion method
이름 그대로 모든 뷰에서 최종 결과를 생성하는 일을 포함해 모든 작업이 완료된 후에 실행됩니다.

![interceptor](/images/interceptor.png)

## 필터와 인터셉터 차이

![filter_interceptor.png](/images/filter_interceptor.png)

### Req/Res 객체 조작 가능 여부

필터는 Req와 Res를 조작할 수 있지만, 인터셉터는 조작할 수 없습니다.

필터가 다음 필터를 호출하기 위해 필터 체이닝(다음 필터 호출)을 해주어야 합니다. 그리고 이때 Req/Res 객체를 넘겨주므로 우리가 원하는 Req/Res 객체를 넣어줄 수 있습니다.

```java
public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) {
        chain.doFilter(request, response)
}
```

하지만 인터셉터는 처리 과정이 필터와 다릅니다.
디스패처 서블릿이 여러 인터셉터 목록을 가지고, 순차적으로 실행시킵니다. 그리고 true를 반환하면 다음 작업을 실행하고 false가 반환되면 요청이 중단됩니다.

```java
default boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) {
        return true;
    }
```