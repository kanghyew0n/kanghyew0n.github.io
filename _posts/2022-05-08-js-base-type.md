---
layout: single
title: "[JavaScript] 타입"
categories:
  - javascript
tags:
  - 자바스크립트  
  - 타입  

---

### 2. 타입 (type)

JavaScript 언어의 타입은 원시 값과 객체로 나뉜다고 한다. 원시값의 종류는 아래와 같다. (BigInt, Symbol은 다음 기회에..)<br/>

- Number 타입 
- String 타입
- Boolean 타입
- Null 타입
- Undefined 타입
- BigInt 타입
- Symbol 타입

<br/>

#### Number  타입 

이름에서부터 티를 내고있다. 숫자형이라고 <br/>

Number  타입에서도 두가지로 표현할 수 있는 유일한 값이 있다고 한다. 그것은 바로바로 `0` 이다. 어떻게 두가지가 되나 하면  `-0`과 `+0` 둘 다로 표현할 수 있다. 둘을 비교했을 때 `+0 === -0`은 참이라고 한다. 하지만 이 사실이 영향을 주는 것은 거의 없다고 한다. (다행이다) 그런데 만약 0으로 나누게 되는 일이 생긴다면 값은 아래와 같이 달라진다.

```
> 42 / +0
Infinity
> 42 / -0
-Infinity
```

<br/>

#### String  타입 

String 타입은 텍스트 데이터 즉 문자를 나타낼 때 사용한다. `''` 또는  `""` 로 감싼 값의 타입은 `string` 이 된다.

```
let age = '24' //String 타입이다.
```

일부 다른 프로그래밍 언어와 달리 JavaScript 문자열은 불변하다. 즉 문자열을 생성하고 바꾸는 것이 불가능하다. 하지만 원본 문자열을 사용하여 새로운 문자열을 생성하는 것은 가능하다고 한다. 

```
let str1 = 'kang'
let str2 = 'hyewon'
let result = str1 + str2

console.log(result) //'kanghyewon'
```

<br/>

**String의 길이 ?**

각각의 요소가 `String`의 한 자리를 차지하여 `String`의 길리는 그 안의 요소 수와 같다.  코드로 확인하고 싶다면 `.length` 로 확인하자!

```
let str = 'hello'
console.log(str.length) // 5
```

<br/>

#### Boolean 타입 

`boolean `타입은 논리요소를 나타내며 `true` 와 `false` 값을 가질 수 있다. 이때 값이 `undefined` 나 `null` 이 아닌 모든 객체는 조건문에서 `true` 값을 가진다. 즉 첫번째 코드의 조건문은 참이 되고, 두번째 코드는 거짓이 된다.

```
let x = new Boolean(false);
if (x) {
  // 이 코드는 실행됨
}
```

```
let x = false;
if (x) {
  // 이 코드는 실행되지 않음
}
```

첫번재 코드 대체 왜 참이냐 하면 원시 `Boolean` 값과 `Boolean` 을 구분해서 알아두어야 하는데 위의 코드에서는 객체를 사용했기 때문이다. 원시 `Boolean` 값의 자리에 `Boolean `객체를 이용해서는 안된다!

```
let x = Boolean(expression);     // 추천 (원시 boolean)
let y = new Boolean(expression); // 사용하지 말것 (boolean 객체)
```

<br/>

**falsy 한 값?**

거짓같은 값의 예시이다. 거짓으로 구분되니 조건문은 실행되지 않는다. 

```
if (false)
if (null)
if (undefined)
if (0)
if (-0)
if (0n)
if (NaN)
if ("")
```

<br/>

#### Null 타입 

Null 타입은 `null` 하나의 값만 가질 수 있다. `null`은 **의도적으로 변수에 값이 없다는 것을 명시**할 때 사용한다. `null`은 글로벌 객체의 속성에 대한 식별자가 아니다. 대신 `null`은 식별되지 않은 것을 표현한다. 즉, 변수가 아무런 객체를 가리키지 않음을 표현합니다. 또한 JavaScript는 대소문자를 구별하므로 null은 Null,NULL 등과 다르다. 

<br/>

#### Undefined 타입 

선언한 후 값을 할당하지 않은 변수 혹은 값이 주어지지 않은 인수에 자동으로 `undefined` 가 할당된다. `null` 과의 차이점은 `undefined`은 변수를 선언하고 값을 할당하지 않은 상태, `null`은 변수를 선언하고 빈 값을 할당한 상태(빈 객체)이다. 즉, `undefined`는 자료형이 없는 상태이다. 쉽게 말해서 `null`은 의도적으로 **너는 값이 없어! **라고 하는 것이고 `undefined` 는 **값이 없는데...?** 라고 생각한다.

```
let x; // 값을 할당하지 않고 변수 선언

console.log(x) // undefined
```

<br/><br/>





**참고 사이트** 

- [데이터타입 - null과 undefined 차이](https://velog.io/@surim014/%EC%9B%B9%EC%9D%84-%EC%9B%80%EC%A7%81%EC%9D%B4%EB%8A%94-%EA%B7%BC%EC%9C%A1-JavaScript%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-part.2) 

- [데이터타입 MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures#%EC%9B%90%EC%8B%9C_%EA%B0%92) 

- [Falsy 한 값](https://developer.mozilla.org/ko/docs/Glossary/Falsy) 

  

<br/><br/><br/>
