# Reflection

리플렉션이란 클래스, 생성자, 메소드, 객체의 정보를, 구체적인 클래스를 모르더라도 접근할 수 있도록 해주는 자바 API입니다.

Reflection을 사용하는 기술들에는 Intellij 자동완성 기능, 어노테이션, 스프링 프레임워크 등에 사용됩니다.

스프링 프레임워크의 어노테이션 기능들이 리플렉션을 통해 프로그램 실행 중 동적으로 클래스의 정보를 가져와서 사용합니다.

스프링에서는 Reflection을 통해 런타임에 개발자가 등록한 빈을 애플리케이션에서 가져와 사용할 수 있게 되는 겁니다.

### 예제

- Object.getClass() : 인스턴스의 클래스 정보를 로드
`Class c = "foo".getClass() //class java.lang.String`
```java
byte[] bt = new byte[1024];
Class cs = bt.getClass(); //class [B
```

배열의 클래스 정보는 타입의 앞글자를 딴 알파벳 하나와 배열의 차원만큼 '[' 가 늘어난다

- .class : 원시타입, 클래스 타입의 클래스 정보를 로드
```java
        boolean wrong;
//        Class cs2 = wrong.getClass(); 컴파일 에러
        System.out.println(boolean.class); //boolean
//        Class cs1 = wrong.class 컴파일 에러
        System.out.println(String.class); //class java.lang.String
	    System.out.println(int[][].class); //class [[I
```
- Class.forName() : 패키지 명으로 클래스 정보를 로드
```java
System.out.println(Class.forName("spring.boot.project.Serialize.Etc"));  
//class spring.boot.project.Serialize.Etc
```
- TYPE Field : 원시타입 클래스 반환 방법
```java
    System.out.println(Double.TYPE); // double  
    System.out.println(Void.TYPE); // void
```
- Method
	- class.getSuperClass() : 슈퍼 클래스를 반환
	- class.getClass() : 상속된 클래스 포함하여 모든 공용 클래스, 인터페이스 및 열거형을 반환
	- class.getDeclaredClass() : 명시적으로 선언된 모든 클래스 및 인터페이스, 열거형을 반환합니다.
	- class.getDeclaringClass() : 클래스에 구성된 클래스(선언된)를 반환
	- class.getEnclosingClass() : 클래스의 즉시 동봉된 클래스를 반환


Reference

https://kingname.tistory.com/164
https://medium.com/msolo021015/%EC%9E%90%EB%B0%94-reflection%EC%9D%B4%EB%9E%80-ee71caf7eec5