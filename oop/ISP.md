# ISP | 인터페이스 분리 원칙 (Interface Segregation Principle)

- 해당 글은 LSP와 추상화를 이해하고 계시면 더욱 이해하기 쉽습니다. LSP와 추상화에 대해 이해하시고 싶으시면  [https://eojil-hyunin-in.tistory.com/3](https://eojil-hyunin-in.tistory.com/3) 이 글을 읽어주세요!

# ISP

ISP에 대해 자세히 알기 전에 위키백과에 나와있는 ISP의 정의부터 알아보죠.

- 인터페이스가 자신이 이용하는 메서드에 의존해야 한다는 원칙

객체지향 설계에서 인터페이스는 객체가 사용하는 메서드를 정의해놓는

일종의 설계도로써의 역할을 가집니다.

## 예시

- 아래 예시들은 기능을 구현하는 클래스들은 인터페이스로부터 구현을 받아야한다는 전제하에 설명된 예시들입니다.

ISP를 지키는 예시를 설명하자면

자동차에 존재하는 기능들은 전진, 후진, 정지, 가속 등등

여러 기능들이 존재합니다.

```java
public interface CarService {
	void go();
	void back();
	void stop();
	void speed();
}
```

이 인터페이스를 구현한 코드는 다음과 같습니다.

```java
public class CarServiceImpl implements CarService {
		public void go() {
			// implements ...
		}
		public void back() {
			// implements ...
		}
		public void stop() {
			// implements ...
		}
		public void speed() {
			// implements ...
		}
}
```

위 메서드들은 모두 **자동차가 사용하는 기능**이죠. 

따라서 필요한 메서드들로만 구현을 하기 때문에 최소한의 코드를 작성할 수 있게 됩니다.

자동차에게 필요한 기능들만 인터페이스에 작성하게 되면 해당 자동차가 어떤 기능을 하는 지

알아보기 쉽고, 인터페이스의 특성상 다중 구현이 가능하기 때문에 메서드를 하나의 책임만을 가지도록 쪼개어 인터페이스를 나눌수록 코드의 재사용성 또한 올라갑니다.

반대로 ISP를 지키지 않는 예시를 들어볼까요?

똑같이 자동차 인터페이스가 있고 자동차가 사용하는 기능들 또한 동일하게 있습니다.

```java
public interface CarService {
	void go();
	void back();
	void stop();
	void speed();
	void fix();
}
```

기존 메서드에 추가로 `fix()` 가 생겼습니다.

해당 기능은 자동차 정비공이 자동차를 분해하여 수리하기 위해 존재하는 기능입니다.

그럼 이제 이 인터페이스를 통해 구현을 해보겠습니다.

```java
public class MechanicServiceImpl implements CarService {
		public void fix() {
			// implements ...
		}
		public void go() {
			// implements ...
		}
		public void back() {
			// implements ...
		}
		public void stop() {
			// implements ...
		}
		public void speed() {
			// implements ...
		}
}
```

해당 코드는 자동차 정비공이  CarService를 `Implements` 받아 구현한 클래스입니다.

자동차 정비공의 역할은 수리를 맡긴 자동차를 그저 수리만 해주면 됩니다.

하지만 `fix()` 메서드가 `CarService` interface에 있기 때문에 다른 메서드들도 번거롭게 구현을 해주어야 합니다. (interface에 정의된 메서드는 모두 구현해야 합니다)  

그렇기에 사용하지도 않는 코드를 해당 클래스에 작성해야하고 시간만 낭비하게 되는 꼴이죠. 

그러니 이 경우에는 `fix()` 메서드를 `MechanicService` 에서 정의하고 `MechanicServiceImpl` 에서 구현해주어야 하는 것이죠.

## 정리

- 인터페이스에는 객체가 행하는 필요한 행위들만 작성한다.
- 필요하지 않는 메소드는 새 인터페이스를 통해 분리한다.
- 인터페이스를 분리하면 책임이 적어지므로 코드의 변경이 드물어지고, 재사용성이 높아진다.