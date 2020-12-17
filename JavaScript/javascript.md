## 변수

#### let 
변수 선언
```js
let name
name = 'monkey'
```

### const

상수 선언
  
 함수를 포함한 대부분의 선언은 모두 const로 한다.
 필요할 경우 let 사용  
 no var.

```JavaScript
const onShowModal = () >= {
    ....    
}
```
### 데이터 타입

 - 별도의 선언 없이 변수에 대입.
 - 숫자, 문자열, boolean, null(값이 없다.), undefined(지정되지 않은 값.)
 - null은 고의적으로 설정 undefined은 설정하지 않은 값

### 비교 연산자
 - === : __두 갑이 타입까지 완전히 일치하는 지 확인__
 - == : 타입은 검사하지 않음
    - 숫자 1과 문자 '1'을 같은 값으로 인식
    - 0과 false도 같은 값으로 인식
    - null과 undefined를 같은 값으로 인식
    - !== : 두 값이 일치하지 않는지 확인

## 함수 

### 함수란?  
  
__특정 코드를 하나의 명령으로 실행해주는 기능__

함수를 만들 때에는 ``function`` 이라는 키워드를 사용, 매개변수를 __파라미터__ 라고 함.

### 문자열 리턴
 - 문자열 조합 시 + 연산자 사용 가능.  
 - __템플릿 리터럴(Template Literal)__ 이란 문법을 사용 가능함.

### 람다 

화살표를 통한 함수를 선언하는 문법

```JavaScript
const add = (a, b) => {
        return a + b;
};
console.log(add(1, 2)); 
```
또한 코드 블럭 내에서 간단하게 한줄로 하나의 리턴을 하는 경우 아래와 같이 줄여 쓴다.
```js
 const add = (a, b) => a + b;
 ```

## Object

### 객체란?

객체는 우리가 변수 혹은 상수를 사용하게 될 때 하나의 이름에 여러 종류의 값을 넣을 수 있게 해준다.

```JavaScript
const dog = {
// 키 : 원하는 값
  name: '멍멍이',
  age: 2
};

console.log(dog.name);  // 멍멍이
console.log(dog.age);   // 2
```
### 함수에서 객체를 파라미터로 받기

```JavaScript
// JS 에서는 카멜케이스 표기법을 사용한다
const ironMan = {
  name: '토니 스타크',
  actor: '로버트 다우니 주니어',
  alias: '아이언맨'
};

const captainAmerica = {
  name: '스티븐 로저스',
  actor: '크리스 에반스',
  alias: '캡틴 아메리카'
};

function print(hero) {
  const text = `${hero.alias}(${hero.name}) 역할을 맡은 배우는 ${
    hero.actor
  } 입니다.`; // 템플릿 리터럴 방식을 사용해서 문자열로 출력
  console.log(text);
}

print(ironMan);
//아이언맨(토니 스타크) 역할을 맡은 배우는 로버트 다우니 주니어 입니다.
print(captainAmerica);
//캡틴 아메리카(스티븐 로저스) 역할을 맡은 배우는 크리스 에반스 입니다.
```

## 객체 비구조화 할당

```js
function print({ alias, name, actor }) {
  const text = `${alias}(${name}) 역할을 맡은 배우는 ${actor} 입니다.`;
  console.log(text);
}
```

파라미터 단계의 객체 비구조화 할당

### 객체 안에 함수 넣기

```js
const dog = {
  name: '멍멍이',
  sound: '멍멍!',
  say: function say() {
    console.log(this.sound);  //여기서 this는 객체 자신을 가리킨다.
  }
};

dog.say();
```
익명 함수를 이용한다면 함수에 이름을 작성하지 않아도 된다.

