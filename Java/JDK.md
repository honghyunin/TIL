# JDK

- Java를 컴파일하고 개발할 수 있도록 하는 개발 환경 세트
    - 개발자만을 위한 컴파일러, 디버깅 툴 제공
    - JRE(+JVM)을 포함한 종합 툴
- Java Development Kit의 약자, 개발자를 위한 자바 개발 도구
- JDK 안에는 JRE, JVM도 포함되어 있습다.

![d](/images/JDK_JRE_JVM.png)

# JVM

- JVM 은 Java가 실제로 동작하는 자바 가상 머신입니다.
- 자바 프로그램이 다양한 OS 혹은 기기에서도 원활히 실행 하게 합니다.
- 메모리를 효율적으로 관리해주는데 이 것이 Garbage Collection 입니다.

# JRE

- Java Runtime Enviorment은 자바 런타임 환경입니다.
- 자바 코드를 실행하기 위한 도구들입니다.
- 자바 클래스 라이브러리/JVM/자바 클래스 로더를 가지고 있습니다.

- 작성된 자바 코드를 JVM에게 넘겨 실행시켜준다.
- 즉, JRE는 JVM이 원활히 작동할 수 있게 환경을 맞춰주는 역할을 합니다.
- JRE는 JVM을 생성하는 Java 디스크 상의 부분입니다.

## JDK 종류

- Java SE (Java Standard Edition)
표준 에디션의 자바 플랫폼 자바 언어의 핵심 기능을 제공입니다.

- Java EE (Java Enterprise Edition)
Java SE 에 웹 어플리케이션 서버에서 동작하는 기능을 추가한 플랫폼입니다.
즉, 서버 측 개발을 하기 위해 필요합니다.
JSP, Servlet, JDBC 등 기업용 애플리케이션을 개발하는 데 필요한 다양한 것들이 포함된 플랫폼입니다.
이 스펙에 따라 제품을 구현한 것을 WAS라 합니다.