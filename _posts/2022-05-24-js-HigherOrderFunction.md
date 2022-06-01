---
layout: single
title: "[JavaScript] 고차함수 이해하기"
categories:
  - javascript
tags:
  - 자바스크립트  
  - 고차함수

---



#### 시작하면서 

고차함수에 대해 이해하기 전에 `일급객체` 에 대해 조금 이해하려고 한다. 사실 일급객체나 고차함수라는 용어는 난생 처음 듣지만 느낌으로는 내가 모르는 새로운 객체나 함수일 것 같았다. 하지만 아니다! 벌써 우린 일급객체를 계속해서 사용해왔던 것이다! 우선, 일급객체의 정의는 

>  일급 객체 (first-class object) 란 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가리킨다  (위키백과..)


그렇다면 다른 객체에 적용한다는 것은 무슨 의미일까? 자바스크립트의 관점에서 보겠다! (난 자바스크립트밖에 모르기때문,,) 다른 객체에 적용한다는 것은

* 변수에 할당할 수 있고 
* 다른 함수의 인자를 전달 받을 수 있고 
* 다른 함수의 결과로서 리턴될 수 있다는 것이다.

그렇다면 일급객체는 `string`, `number`, `boolean`, `object`, `array`...타입들의 데이터를 말할 수 있고 함수도 일급 객체가 된다. 우리는 함수 `선언식`과 `표현식`으로 사용하는데 표현식 같은 경우 변수에 할당하기 때문에 일급객체가 되는 것이다! *물론 자바스크립트에서만 함수가 일급객체이다.* (아래 코드는 함수 표현식임)

```js
var funcName = function () {
  
};
```

<br/>

근데 왜 고차함수에서 일급객체에 대해 짚고 넘어가느냐! 

위에서 설명했듯 함수는 변수에 할당할 수 있다. 그리고 함수는 함수를 담은 변수를 전달인자로 받을 수 있다. 따라서 함수가 `일급객체`이기 때문에 `고차함수`를 만들 수 있고 `콜백`을 사용할 수 있다. (설명은 밑에서)



### 고차함수 (higher order function) 이해하기 

`고차 함수` (higher order function)는 함수를 전달인자 (argument) 로 받을 수 있고, 함수를 리턴할 수 있는 함수이다.  이때! 다른 함수의 전달인자로 전달되는 함수를 콜백함수 (callback function) 이라고 한다.

즉, 고차함수에서 전달인자가 되는 함수가 콜백함수인 것이다. 어떤 작업이 완료되었을 때 호출하는 경우가 많아서 답신전화를 뜻하는 콜배함수라고 한다나 .. 

'함수를 리턴하는 함수' 라는 장난스러운 모양새는 따로 부르는 이름이 있다. 이를 고안해 낸 논리학자 하스켈 커리(Haskell Curry)의 이름을 따, 커링 함수라고 한다. 그럼 커링함수 = 고차함수 라고 생각할 수도 있지만 고차함수가 커링함수를 포함하고 있다고 생각하면 된다.

그렇다면 고차함수의 모양새를 보겠다!



1. 다른 함수를 인자로 받는 경우 

 * 함수 higher은 다른 함수를 인자로 받는 고차 함수입니다.
 * 함수 higher의 첫 번째 인자 callback에 함수가 들어올 경우
 * 함수 callback는 함수 higher의 콜백 함수입니다.

```js
function callback(num) {
  return num + 1;
}

function higher(callback, num) {
  return callback(num);
}

//  * 아래와 같은 경우, 함수 func은 함수 higher의 콜백 함수다.
let output = higher(callback, 2);
console.log(output); // -> 3
```

<br/>

2. 함수를 리턴하는 경우
* 함수 higher는 다른 함수를 리턴하는 고차 함수입니다.
* higher는 인자 한 개를 입력받아서 함수(익명 함수)를 리턴합니다.
* 리턴되는 익명 함수는 인자 한 개를 받아서 added와 더한 값을 리턴합니다.

```js
function higher(added) {
  return function (num) {
    return num + added;
  };
}

// adder(5)는 함수이므로 함수 호출 연산자 '()'를 사용할 수 있다.
let output = higher(5)(3); // -> 8
console.log(output); // -> 8

// adder가 리턴하는 함수를 변수에 저장할 수 있다.
// javascript에서 함수는 일급 객체이기 때문
const add3 = higher(3);
output = add3(2);
console.log(output); // -> 5
```

<br/>



### 내장 고차함수 알아보기 

자바스크립트에는 기본적으로 내장된 고차함수가 있다. 그중에서도 배열 메스드들 중 일부가 대표적인 고차함수에 해당한다.  `filter` , `map` , `reduce` 에 대해 알아보잣!



#### filter

이름에서도 무슨 역할인지 티가 난다. 배열의 `filter` 메서드는 모든 배열의 요소 중에 특정 조건을 만족하는 요소를 필터처럼 걸러준다. 뭐 예를 들면 배열에서 `number` 타입만 걸러내겠다! 혹은 짝수만 걸러내겠다! 하면 쉡게 걸러낼 수 있다.  밑에서 사용방법을 간단하게 보자. 

```js
let arr = [1, 2, '강혜원', 4, 5];
let output = arr.filter(짝수만 걸러내줘);
console.log(output); // ->> [2, 4]

output = arr.filter(문자열만 걸러내줘)
console.log(output); // ->> ['강혜원']
```

<br/>

여기서 filter안에 괄호는 함수 형태다. (내장 고차함수니까 함수를 전달인자로 가지고 있다.)  물론 함수를 따로 선언한 후 함수를 부르는 방법도 있지만 괄호 안에서 선언할 수도 있다.(밑에서 확인해보자)

```js
// 함수 표현식
const isEven = function (num) {
  return num % 2 === 0;
};

let arr = [1, 2, '강혜원', 4, 5];

let output = arr.filter(isEven);
console.log(output); // ->> [2, 4]
```

```js
let arr = [1, 2, '강혜원', 4, 5];

let output = arr.filter(function (el) {
    return el % 2 === 0;
});
console.log(output); // ->> [2, 4]
```

<br/>

둘의 의미는 같지만 아래의 코드가 훨씬 간편하다는 사실!

filter에서 사용되는 콜백함수는 일회성이 강하기 떄문에 따로 선언하는 것 보다는 익명함수로 사용하는게 좋을 것 같다!



#### map

`map`은 사실 이름만 봐서는 긴가민가하다. `map`은 배열 내의 모든 요소에 각각에 대해 주어진 함수를 호출한 결과를 모아서 새로운 배열을 반환한다!

그말은 for문을 이용하지 않아도 배열에 있는 모든 요소에 접근하여 함수를 적용시킬 수 있다는 것이다! 뭐 `number` 타입으로 구성된 배열의 요소들에게 +2 를 해서 다시 새로운 배열을 반환해! 라고 하면 for문으로 배열의 요소 하나하나에 접근 해서~ +2 씩 해주고 다시 새로운 배열에 담아주고~ 를 하지 않아도 된다는 점! 그렇다면 밑에서 사용방법을 보자보자 

```js
let arr = [1, 2, 3, 4, 5];

let output = arr.map(function (el) {
    return el + 2;
});
console.log(output); // ->> [3, 4, 5, 6, 7]
```

<br/>

*여기서 잠깐!*

괄호안에 들어가는 콜백 함수를 화살표 함수로 표현하면 더욱 간단해진다.

```js
let arr = [1, 2, 3, 4, 5];

let output = arr.map(el => el + 2);
console.log(output); // ->> [3, 4, 5, 6, 7]
```

<br/>

#### reduce

`reduce` 는 이름만 보면 뭔가 줄이는 것 같다. 뭐 비슷한 느낌이긴 하다. `reduce`는 여러 데이터를 하나의 데이터로 응축할 때 사용한다. 응축한다는 것은 와닿지 않을 수 있으니 .... 평균을 내는 것처럼 누적값을 반환해준다! 라고 생각하면 조금 이해가 간다.

다른 내장고차함수와 다르게 `reduce` 함수는 4개의 인자를 가진다. 

* 누산기 (acc)
* 현재 값 (cur)
* 현재 인덱스 (idx)
* 원본 배열 (src)

`reduce` 함수의 반환 값은 누산기에 할당되고, 누산기는 순회 중 유지되므로 결국 최종 결과는 하나의 값이 된다. 말로는 어려우니 사용법을 바로보자!

```js
const addAccCur = function (acc, cur) {
  return acc + cur;
};
const initialValue = 1;

let arr = [1, 2, 3, 4, 5];
let output = arr.reduce(addAccCur, initialValue);
console.log(output); // ->> 16
```

```js
let arr = [1, 2, 3, 4, 5];

let output = arr.reduce(function (acc, cur) {
    return acc + cur;
}, 1);
console.log(output); // ->> 16
```

<br/>

위의 코드와 아래의 코드가 많이 달라보이지만 같은 의미다! `filter` 와 `map`과 가장 달라보이는 것은 초기값인 것 같다. `reduce`에서 초기값의 유무에 따라서 값이 완전 달라지기 때문이다. 우선, acc는 누적값이고 cur은 현재 값이다. 누적값을 저렇게 표현했지만 `acc = acc + cur` 이라고 생각하면 조금 이해가 될 것이다. 

만약 초기값이 없다면! 최초의 누적값 (acc)은 무엇일까? 초기값이 없기 때문에 첫번째 현재값 (cur) 이 될것이다. 그렇다면 위의 코드에서는 배열의 첫번째 요소인 1 이 첫번째 acc 가 되는 것이다. 그렇다면 결과는 [1, 2, 3, 4, 5] 를 전부 합한 15가 된다.

하지만 위의 코드처럼 초기값이 1이라면 최초의 누적값 (acc)은 무엇일까? 초기값이 1이면 첫번째 누적값에 1이 먼저 들어갈 것이다. 그렇다면 결과는 (*직관적으로 표현해본다면*)  [1, 1, 2, 3, 4, 5] 를 전부 합한 16이 된다.

<br/>

### 고차함수를 왜 사용할까?

고차함수는 함수 즉 사고의 묶음을 전달받아서 처리한다. 이는 함수에 대한 복잡한 로직이 감춰지기 때문에 추상화라고 볼 수 있다!  고차함수는 사고의 추상화인 것이다. 그렇다면 함수도 아닌 고차함수를 사용하는 이유는? 함수를 보면 알 수가 있다. 함수는 값을 전달받아서 처리한다. 따라서 값에대한 복잡한 로직이 감춰진다고 할 수 있다. 함수는 값 수준에서의 추상화인 것이다! 

추상화는 내부 구조에 대한 고민을 줄이고 문제해결이 쉬워져 생산성이 향상된다. 사고의 추상화(고차함수) / 값 수준에서의 추상화(함수) 둘을 비교해보면 사고의 추상화에서 수준이 높아진 만큼 생산성도 상승한다고 할 수 있다. 


<br/>
<br/>

**참고 사이트**

* [일급 객체](https://ko.wikipedia.org/wiki/%EC%9D%BC%EA%B8%89_%EA%B0%9D%EC%B2%B4) 
* [고차함수](https://poiemaweb.com/js-array-higher-order-function) 
* [filter (MDN)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
* [map (MDN)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
* [reduce (MDN)](https://ko.wikipedia.org/wiki/%EC%9D%BC%EA%B8%89_%EA%B0%9D%EC%B2%B4)



<br/>

<br/>



















