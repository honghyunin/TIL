## 변수

#### let 
변수 선언
```js
let name
name = 'monkey'
```

### const

상수 선언
  
 함수를 포함한 대부분의 선언은 모두 const로 합니다.
 필요할 경우 let 사용 합니다.

```JavaScript
const onShowModal = () >= {
    ....    
}
```
### 데이터 타입

 - 별도의 선언 없이 변수에 대입합니다
 - 숫자, 문자열, boolean, null(값이 없다.), undefined(지정되지 않은 값.)
 - null은 고의적으로 설정 undefined은 설정하지 않은 값입니다

### 비교 연산자
 - === : __두 갑이 타입까지 완전히 일치하는 지 확인__ 합니다.
 - == : 타입은 검사하지 않습니다.
    - 숫자 1과 문자 '1'을 같은 값으로 인식합니다.
    - 0과 false도 같은 값으로 인식합니다.
    - null과 undefined를 같은 값으로 인식합니다.
    - !== : 두 값이 일치하지 않는지 확인합니다.

## 함수 

### 함수란?  
  
__특정 코드를 하나의 명령으로 실행해주는 기능__ 입니다.

함수를 만들 때에는 ``function`` 이라는 키워드를 사용, 매개변수를 __파라미터__ 라고 합니다.

### 문자열 리턴
 - 문자열 조합 시 + 연산자 사용 가능.  
 - [__템플릿 리터럴(Template Literal)__](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals) 이란 문법을 사용 가능합니다.

### 람다 

화살표를 통한 함수를 선언하는 문법은 다음과 같습니다.

```JavaScript
const ex = (a, b) => {
        return a + b;
};
console.log(ex(1, 2)); 
```
또한 코드 블럭 내에서 간단하게 한줄로 하나의 리턴을 하는 경우 아래와 같이 줄여 씁니다.
```js
 const ex = (a, b) => a + b;
 ```

## 객체

### 객체란?

객체는 배열과 같은 기능을 공유하지만, 객체는 이름으로 데이터를 분류한다. 또한 하나의 이름에 여러 종류의 값을 넣을 수 있게 해줍니다.

```JavaScript
const hyunin = {

  name: '현인',
  age: 17
};

console.log(dog.name);
console.log(dog.age);
```
### 함수에서 객체를 파라미터로 받기

```JavaScript
// JS 에서는 카멜케이스 표기법을 사용한다
const Joker = {
  Actor: 'Joaquin Phoenix',
  role : 'Joker',
  age : '46'
};



  function print(line){
    const text = 
    ` 조커의 ${Joker.role} 역할을(를) 
     ${Joker.Actor} 이고, 나이는 ${Joker.age} 이다.`; 
     console.log(text); 
     }

print(Top);
//  조커의 조커를 맡은 Joaquin Phoenix 이고, 나이는 46 이다.

```

## 객체 비구조화 할당

```js
function print(Actor, role, age) {
  const text = `조커의 ${role} 역할을(를) 
     ${Actor} 이고, 나이는 ${age} 이다.`;
  console.log(text);
}
```

파라미터 단계의 객체 비구조화 할당입니다

### 객체 안에 함수 넣기

```js
const Hyunin = {
  name: '현인',
  sing: 'sing a song!',
  sing: function sing() {
    console.log(this.sing);  //여기서 this는 객체 자신을 가리킵니다.
  }
};

Hyunin.sing();

// 출력 결과 : [Function : sing]
```
익명 함수를 이용한다면 함수에 이름을 작성하지 않아도 됩니다. 


## (변수 ``` 재선언 가능```)

```js
var variable = '변수선언';
console.log(variable); // 변수 선언한 것입니다

var variable = '또 변수선언함';
console.log(variable); // 또 변수 선언한 것입니다
```
변수 선언을 여러 번해도 다른 값이 출력되므로 동일한 변수명을 남용하는 문제가 발생합니다.

## let (변수 ```재선언 불가능```, 변수 ```재할당 가능```)

```js
let variable = '변수선언함'; console.log(variable); //변수 선언한 것입니다.
 variable = '변수 재할당함'; console.log(variable); 
 //변수 재할당한 것입니다.
 let variable = '또 변수선언함'; console.log(variable); //또 변수 선언한 것입니다.
```
## const ( 변수 ```재선언 불가능```, 변수 ```재할당 불가능```)

```js
const variable = '변수선언함'; console.log(variable); //변수 선언한 것
variable = '변수 재할당함'; console.log(variable);
 //변수 재할당한 것(에러)
  const variable = '또 변수선언함';
   console.log(variable); //또 변수선언한 것(에러)
```

# 결론 

재할당이 필요없는 경우, const를 사용해 불필요한 변수의 재사용을 지양하고, 재할당이 필요한 경우 let을 사용하는 것이 좋습니다.