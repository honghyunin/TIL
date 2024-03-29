# LSP | 리스코프 치환 원칙 (Liskov Substitution Principle)

- 부모 클래스를 상속받은 자식 클래스로도 부모 클래스의 메소드들을 동작할 수 있어야 하는 원칙이다. 다시 말해 부모 클래스로 짜인 코드를 자식 클래스로 변경하였을 때도 원활하게 프로그램이 동작할 수 있어야 합니다.

# 예시

- 예를 들어 부모와 자식이 있습니다. 부모는 자동차를 운전할 줄 압니다. 자식은 운전하는 방법을 부모로부터 습득(상속)합니다. 부모로부터 운전하는 방법을 습득한 자식은 부모 대신 운전을 할 수 있어야 합니다.

리스코프 치환 원칙에 대해 알아보기 위해,

원칙을 위반하는 동물/고양이 예제를 통해 알아봅시다.

```java
public class Animal {

public String getName() {
	return "Animal";
	}
}

public class Cat extends Animal {

@Override
public String getName() {
	return "Cat"
	}
}
```

Animal이라는 클래스와 이를 상속하는 Cat이라는 클래스가 있습니다. Animal 클래스는 자신의 이름을 가지고 각각 getter를 가집니다.

Animal에서 `getName()` 실행할 경우 “Animal” 을 반환하고

Cat에서 `getName()`을 실행할 경우 “Cat”을 반환합니다.

자 해당 코드를 테스트해봅시다.

```java
Animal animal = new Animal();

checkAnimal(animal) // true

Animal cat = new Cat();

checkAnimal(cat) // false
```

테스트 결과 부모 클래스로 `checkAnimal`을 실행했을 때 true지만,

자식 클래스로 `checkAnimal`을 실행했을 때 false가 나옵니다.

이 경우 이 코드는 리스코프 치환 원칙을 위반한 것입니다.

> 왜 굳이 부모 클래스를 상속받은 자식 클래스도 부모 클래스의 코드를 원활하게 실행시켜야 하나요?  
> 그럼 굳이 자식 클래스를 사용하는 이유가 없지 않나요?

물론 부모 클래스의 코드만 자식 클래스가 원활하게 실행시키기 위함이었으면 이 원칙이 생기지 않았겠죠.

이유는 SOLID 원칙에는 개방 폐쇄의 원칙이 존재하는데요.

기존의 코드를 수정하지 않고 새로운 기능을 추가하고 수정할 수 있어야 하는 원칙입니다.

때문에 상속받은 자식 클래스에서 부모 클래스의 기능을 유지하면서 기능의 추가와 수정을 이루는 것입니다.

그렇기 때문에 기능을 추가하거나 수정을 하기 위해 부모 클래스를 상속받은 자식 클래스를 통해서 새로운 기능을 추가하면 기존의 코드는 변경되지 않고 OOP 원칙을 모두 잘 지킬 수 있겠죠.	