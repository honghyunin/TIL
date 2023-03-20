# PSA

> Portable Service Abstraction : 휴대용 서비스 추상화라는 의미 

환경의 변화와 관계없이 일관된 방식의 기술로의 접근 환경을 제공하는 추상화 구조를 말한다

추상화 계층을 추가해 서비스를 추상화시키고 여러 서비스를 비즈니스 로직을 수정하지 않고 교체할 수 있도록 하는 것이다

이는 POJO 원칙을 철저히 따른 Spring의 기능으로 Spring에서 동작할 수 있는 라이브러리들은 POJO원칙을 지키게끔 PSA형태의 추상화가 되어있음을 의미합니다.

# Spring Web MVC

## 일반적인 서블릿 형태

```java
public class CocoServlet extends HttpServlet {
 
	// GET
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		super.doGet(req, resp);
	}
	
	// POST
	@Override
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		super.doPost(req, resp);
	}
}
```

## Spring Web MVC의 형태

```java
@Controller
class UserController {
 
	@GetMapping("/user")
	@LogExecutionTime
	public String getUser(@RequestParam name: String) {
		return userRepository.findByName(name);
	}
	 
	@PostMapping("/user/signUp")
	@LogExecutionTime
	public String processCreationForm(@RequestBody signUpDto: SignUpDto) {
		return userRepository.save(signUpDto.toEntity()).getId();
	}
}
}
```

일반 클래스에 @Controller 어노테이션을 사용하면 요청을 매핑할 수 있는 컨트롤러 역할을 수행하는 클래스가 된다.

그 클래스에는 @GetMapping과 @PostMapping 어노테이션을 사용해서 요청을 매핑할 수 있다

그 클래스에는 @GetMapping과 @PostMapping 어노테이션을 사용해서 요청을 매핑할 수 있다
- 서블릿을 Low Level로 개발하지 않고도, Spring Web MVC를 사용하면 이렇게 서블릿을 간편하게 개발할 수 있다. 그 이유는 **name뒷단에 Spring이 제공해주는 여러 기능들이 숨겨져 있기 때문이다**
- 즉, HttpServlet을 상속받고 doGet(), doPost()를 구현하는 등의 작업을 하지 않아도 되는 것이다.

Service Abstraction(서비스 추상화)의 목적 중 하나가 이러한 편의성을 제공하는 것입니다.

# Spring Transaction

Low level로 트랜잭션 처리를 하는 간단한 예제 코드이다.

```java
 try (Connection conn = DriverManager.getConnection(
             "jdbc:coco://127.0.0.1:5432/test", "coco", "password");
             Statement statement = conn.createStatement();
             ) {
             
             //start transaction block
             conn.setAutoCommit(false); //default true
             
             String SQL = "INSERT INTO User " +
             			  "VALUES (171, 50, 'GodanSee')";
             stmt.executeUpdate(SQL);
             
             String SQL = "INSERTED INT Employees " +
             			  "VALUES (187, 82, 'Juntiy')";
             stmt.executeUpdate(SQL);
             
             // end transaction block, commit changes
             conn.commit();
             
             // good practice to set it back to default true
             conn.setAutoCommit(true);
             
             } catch(SQLException e) {
             	
                log.info(e.getMessage());
                conn.rollback();
             }
```

setAutoCommit(false)를 통해 자동커밋을 막아주고, 오류 없이 진행된다면 commit(), exception이 발생하면 rollBack() 롤백하는 코드이다

위와 같이 Low Level로 트랜잭션 처리를 하려면 명시적으로 setAutoCommit()과 **commit(), rollback()**을 호출해야 한다.

하지만 Spring이 제공하는 @Transactional 어노테이션을 사용하면 단순하게 어노테이션을 붙여줌으로써 트랜잭션 처리가 간단하게 이루어진다

```java
@Transactional(readOnly = true)
User findByName(String name);
```

### **3. Spring Cache**

Cache도 마찬가지로 JCacheManager, ConcurrentMapCacheManager, EhCacheCacheManager와 같은  
여러가지 구현체를 사용할 수 있다.

```less
@Transactional
@Cacheable("users")
List<User> findAllUser();
```

사용자는 **@Cacheable** 어노테이션을 붙여줌으로써 구현체를 크게 신경쓰지 않아도 필요에 따라 바꿔 쓸 수 있습니다.  
  
Spring은 이렇게 **특정 기술에 직접적 영향을 받지 않게끔 객체를 POJO 기반으로 한번씩 더 추상화한 Layer를 갖고 있으며,**  
**이를통해 일관성있는 Service Abstraction(서비스 추상화)를 만들어 냅니다.**  
덕분에 코드는 더 견고해지고 기술이 바뀌어도 유연하게 대처할 수 있게 됩니다.


## Refrence
- [[Spring] PSA(Portable Service Abstraction)란?](https://dev-coco.tistory.com/83)
- [[Spring] 스프링 PSA](https://atoz-develop.tistory.com/entry/Spring-%EC%8A%A4%ED%94%84%EB%A7%81-PSA)