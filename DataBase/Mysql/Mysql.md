# SQL

- __Structured__ 구조화
- __Query__ 질의 (CRUD를 DB에게 요청)
- __Language__ 공통의 약속(언어)  

*table* ↔️ column, 열  == 데이터구조  
*table* ↕️ row, record, 행 == 데이터자체


# MySql의 구조

- MySql은 엑셀과 같이 스프레드 시트처럼 데이터를 저장합니다.
- __표(table)__ 는 데이터들을 저장하는 곳입니다.
- __스키마(Schema)__ 는 표를 그룹화한 것입니다. 
- __데이터베이스 서버(Database Server)__ 는 Schema를 보관하는 저장소입니다.


# MySql Command

## 테이블 생성

예시) 
```m
> CREATE TABLE TableName(
  name type(maximum number)  
  id INT(11) NOT NULL AUTO_INCREMENT, 
  title VARCHAR(100) NOT NULL,
  description TEXT NULL,
  created DATATIME NOT NULL,
  author VARCHAR(30) NULL,
  profile VARCHAR(100) NULL,
  PRIMARY KEY(id);  
)  
```
  
  
__특징__
```
- NULL : 공백 가능합니다
- NOT NULL : 공백 불가능합니다
- AUTO_INCREMENT : 입력되는 데이터의 id값을 1씩 증가합니다
- PRIMARY key : 중복이 되지 않는 고유한 값입니다
```
<br><br>

## 입력 

```
INSERT INTO TableName (columnName, columnName2, ...) VALUES('lorem', 'lorem', '...');
```

## 출력
```
SELECT columnName1, columnName2 ... FROM tableName; 

FROM : 어디에서(tablename,columnname ...)
WHERE : 조건
ORDER BY columnName : 정렬해서 출력합니다.
```