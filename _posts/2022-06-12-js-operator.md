---
layout: single
title: "[JavaScript] 연산자"
categories:
  - javascript
tags:
  - 자바스크립트  
  - 연산자

---



### 삼항 연산자 

* 3개의 피연산자, 조건 연산자 (if문과 비교)

```js
const val = (조건) ? 참일때 : 거짓일때 
const val = (조건) ? ((조건) ? 참일때 : 거짓일때) : 거짓일때 //-> 중첩도 사용가능 

if (조건) {
    val2 = 참일때;
} else {
    val2 = 거짓일때;
}
```

```js 
const age = 20;
const isAdult = age >= 20 ? '성인' : '미성년자';

isAdult; //-> '성인' 
```

<br/>

**그렇다면 삼항 연산자와 if문의 차이는?**

* 삼항연산자 : (값, 식, 문) 중 (값, 식) 만 들어올 수 있다 -> 조건과 참, 거짓을 작성할 때 
* if문 : for문, while문 등등 함께 사용이 가능함 



### typeof 연산자 

* primitive : string, number, bigint, boolean, undefined, symbol, null

```js
const str = 'string';
const func = function() {};

typeof str; //-> 'string'
typeof 123; //-> 'number'
typeof 1n; //-> 'bigint'
typeof true; //-> 'boolean'
typeof Symbol(); //-> 'symbol'
typeof undefined; //-> 'undefined'
typeof func; //-> 'function'
```

```js
typeof []; //-> 'object'
typeof {}; //-> 'object'
typeof null; //-> 'object'
typeof new Boolean(true); //-> 'object'
// 참조객체로 만든 것으로 원시값을 만들어내도 참조객체로 나옴 
```

* null : 원시값인데 참조값처럼 type이 'object'가 나옴 
* null -> 객체로 인식 -> 자바스크립트 초기 설계 오류 !



### instanceof 연산자 

* 객체의 인스턴스를 확인하기 좋음 
* 즉 객체의 인스턴스가 어떤 생성자로 생성된 것인지 파악 가능 

```js
const obj = {};
const arr = [];
const func = function() {};

obj instanceof Object; //-> true
arr instanceof Array; //-> true
func instanceof Function; //-> true

undefined instanceof Object; //-> false
null instanceof Object; //-> false -> 원시값임을 증명함!
```

```js
obj instanceof Object; //-> true
arr instanceof Object; //-> true
func instanceof Object; //-> true
// 프로토타입 최상위인 객체로 비교를 하면 true로 나옴 !
```



### 기타 연산자 

* void 연사자 -> 표현식 

```js
void 1; //-> undefined
void 10; //-> undefined

function voidFunc() {
    return undefined; // 이런 느낌 , undefined를 일부러 주기위해 사용됨 
};
```

```html
<a href="javascript:void(0)" id="loginlink">login</a>
```

* 비어있는 링크를 걸어야 할 때 사용함 
* 전에는 자주 사용했지만 요즘엔 사용 잘 안함 

<br/>

<br/>

























