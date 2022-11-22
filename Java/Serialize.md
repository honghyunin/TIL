# 직렬화 Serialize / 역직렬화 Deserialize
> 자바내부에서 사용되는 데이터를 자바 코드 밖에서 쓸 수 있도록 해주는 것이다.

**직렬화**는 자바 코드 내부에서 사용되는 Object 와 같은 클래스와 객체, 데이터를 자바시스템 외부에서도 사용할 수 있도록 byte 형태의 데이터로 변환하는 기술이다.

다시말해 JVM의 메모리에 상주되어있는 객체 데이터를 바이트 형태로 변환하는 기술.

직렬화를 통해 객체를 파일로 저장하거나 전송하고자 할 때 사용된다.

**역직렬화**는 직렬화와 반대로 직렬화된 파일 등을 역으로 직렬화해 다시 객체 형태로 변환하여 JVM내의 상주하도록 복원하는 기술이다.


## 직렬화 방법

- 직렬화 할 클래스에 `Serializable` 를 구현 클래스로 만든다.

```java
public class Member implements Serializable {

...
}
```

#### 직렬화 대상 제외

`Serializable` 를 가진 클래스를 직렬화하면 모든 멤버가 직렬화된다.

하지만 특정 멤버를 제외할 수가 있다.

``` java
public class Member implements Serializable {
	private String id;
	private String name;
	private transient String password;
}
```

위와 같이 `transient` 키워드를 달아주면 된다.

#### 기본 자료형이 아닌 멤버가 있는 경우

primitive type이 아닌 다른 객체를 멤버로 가지는 경우에 모든 멤버를 `Serializable` 구현 클래스로 만들어줘야 한다. 멤버들 중 하나라도 구현한 클래스가 없다면 직렬화할 수 없다.

## 구현

**직렬화**
```java
Member member = new Member("현인", "honghyunin", 1L, new Etc(), new Something());  
  
byte[] serializeMember;  
  
ByteArrayOutputStream baos = new ByteArrayOutputStream();  
ObjectOutputStream oos = new ObjectOutputStream(baos);  
  
oos.writeObject(member);  
  
serializeMember = baos.toByteArray();  
System.out.println("SerializeMember : " + Base64.getEncoder().encodeToString(serializeMember));
```

**역직렬화**

```java
String base64Member = "Member ";  
  
byte[] serializeMemberByte = Base64.getDecoder().decode(base64Member);  
  
ByteArrayInputStream bais = new ByteArrayInputStream(serializeMemberByte);  
ObjectInputStream ois = new ObjectInputStream(bais);  
  
Object objectMember = ois.readObject();
Member member = (Member) objectMember;  
System.out.println("Member : " + member);
```