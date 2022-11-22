# Getter/Setter

Getter/Setter는 객체의 값에 접근하여 값을 가져오거나, 수정하기 위해 필요한 것입니다

```java
	public String getUsername() {
		return this.username;
	}

	public String setUsername(String username) {
		this.username = username;
	}
```


# Backing Field

Kotlin의 필드는 기본적으로 getter/setter를 가집니다 따라서 기본적인 getter/setter를 클래스 내부에서 각각 선언하지 않고도 있는 것처럼 객체에 접근하여 값을 가져오고 수정할 수 있습니다.

```kotlin
var name: String = "hyunin"

println(field) // field.getField()를 호출하고 있는 것
field = "hong" // 자바에서 a = 2를 통해 값을 변경하는 것이 아닌, 내부에서 setter를 통해 값을 변경하고 있는 것이다.
println(field) // hong
```

위 코드에서 `println(field)` 와 같이 값을 불러올 때 getter가 호출되고 `field = "hong"` 값이 값을 변경할 때는 setter를 호출하여 객체의 프로퍼티를 다룹니다.

또한 객체를 `val name : String` 과 같이 선언할 경우 불변성을 지니기 때문에 `name = "hyunin"` setter를 통해 값을 변경할 수 없어 데이터 무결성을 지킬 수 있습니다.
