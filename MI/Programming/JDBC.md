# JDBC 동작 흐름

1. JDBC 드라이버 로드
2. DB 연결
3. DB에 데이터를 읽거나 쓰기
4. DB 연결 종료

## JDBC 드라이버

- DBMS와 통신을 담당하는 자바 클래스
- DBMS 별로 알맞은 JDBC 드라이버 필요(jar)
- 로딩코드 : **Class.forName("JDBC드라이버 이름");**

## JDBC URL

- DBMS와의 연결을 위한 식별 값

# 실제로 실행된 쿼리의 형태를 보여주는 코드

스프링부트에서는 application.properties, application.yml 등의 파일로 **한 줄의 코드로 설정**할 수 있도록 지원하고 권장하니 이를 사용하겠습니다.

src/main/resources/ 에 [application.properties](http://application.properties) 란 파일을 만들어

``spring.jpa.show_sql=true`` 다음의 내용을 작성하면 콘솔에서 쿼리 로그를 확인할 수 있습니다.