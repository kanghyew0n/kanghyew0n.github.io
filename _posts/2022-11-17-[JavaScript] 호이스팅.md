# 호이스팅

- 호이스팅이란 "끌어올린다" 라는 뜻으로
- 변수 및 함수 선언문이 스코프 내의 최상단으로 끌어올려지는 현상 을 말한다.
- 자바스크립트는 모든 선언에 호이스팅이 일어난다.

( 여기서 주의할 점은 "선언문" 이라는 것이며 "대입문"은 끌어올려지지 않는다. )  

<br/>

```jsx
console.log(a);
var a = 2;
```

> var는 선언, 초기화가 동시에 이루어지기 때문에 undefined를 출력하지만  
let,const는 선언단계만 호이스팅 되기 때문에 Reference Error를 출력한다.
> 

- var는 선언과 동시에 undefined로 초기화 하여 메모리에 저장한다. → 호이스팅이 일어난다.
- let, const는 초기화 되지 않은 상태로 메모리에 저장된다. → 초기화 되지 않으면 레퍼런스 에러가 발생한다.

<br/>

```jsx
func();
function func() {
  console.log('함수 호이스팅');
}
```

> 함수 호이스팅 → 출력


<br/>

```jsx
func();
var func = function() {}
```

- 함수표현식은 호이스팅 되지 않는다.
- 여기서는 변수 func의 호이스팅이 발생해서 참조할 수는 있기 때문에 ReferenceError가 발생하지 않지만 그 값이 `undefined`이기 때문에 TypeError가 발생한다.

<br/>

```jsx
func();
var func = function(){ console.log('변수 호이스팅') }
function func() {
  console.log('함수 호이스팅');
}
```
* 함수 선언문과 변수 선언문(함수 표현식)이 있지만 함수 선언문이 먼저기때문에 "함수 호이스팅"이 출력된다!
* 만약 변수 선언문이 먼저라면 TypeError가 발생해야함! 


<br/>
<br/>
