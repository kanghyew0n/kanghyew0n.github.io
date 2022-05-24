---
layout: single
title: "[JavaScript] 변수"
categories:
  - javascript
tags:
  - 자바스크립트  
  - 변수  
---

#### 시작하면서

자바스크립트란 웹사이트의 동적인 부분을 담당한다. HTML로 구조를 만들고 CSS로 디자인을 하며 로그인이나 스크랩과 같은 기능을 자바스크립트로 작성한다고 생각하자!

비유하자면 몸의 근육이나 건축하는 작업과 같은 느낌



### 1. 변수 (Variable)

변수란 말 그대로 변하는 수로 숫자나 문자열과 같은 데이터를 보관하는 박스라고 생각할 수 있다. 숫자가 변하기 때문에 재사용도 가능하다.

사용방법은 **1. 선언하고** (데이터를 담을 박스를 준비)   **2.** **값을 할당해주는** (박스 안에 데이터 넣기) 것

예를 들어 구구단을 출력하기 위해서는 2 x 1, 2 x 2, 2 x 3, 2 x 4, 2 x 5 ...이렇게 9단까지 긴 여정을 거쳐야한다.

```js
console.log(2 * 1) 
console.log(2 * 2)
console.log(2 * 3) 
console.log(2 * 4) 
console.log(2 * 5)
console.log(2 * 6) 
console.log(2 * 7) 
console.log(2 * 8)
console.log(2 * 9) 
```

(이 과정을 8번 더 반복해야 함)

변수를 사용하면 어떻게 간단해질까?

 

#### 변수의 선언

변수를 본격적으로 사용하기 전에 필요한 것은 선언! 무언가를 담기 위해서는 담을 용기부터 준비해야한다.

선언하는 방법은 1. 키워드를 입력하고  2. 변수명을 정한다.

```js
let name;
let age;
```

만약 1번을 건너뛰고 2번부터 한다면 (예를 들어 아래와 같이)

```js
name;
age;
```

`undefined` 라는 값을 받게 되고 오류를 부르니 조심하자



#### 변수의 할당

변수라는 공간을 마련했다면 값을 넣으면 된다. 방법은 간단하다.

할당 연산자 (=) 를 사용한다. 할당하지 않을 경우 `undefined` 가 할당된다.

```js
let name; //선언
name = kanghyew0n; //할당

let age; //선언
age = 24; //할당
```

아래와 같이 간단하게 선언과 할당을 동시에 할 수 있다.

```js
let name = kanghyew0n;
let age = 24;
```



#### 변수의 사용 

그렇다면 어떻게 변수를 사용하여 구구단을 간단하게 출력할 수 있을까?

구구단 1단에서 9단까지 변하는 값을 변수로 설정하고, 그 변수만 바꿔준다면 구구단 전체를 출력하는 것 보다 간단한 코드가 된다! 아래 코드에서 마지막 줄의 `num`  값만 바꿔주면 구구단 완성!

```js
let num; //변수의 선언 

console.log(num * 1) 
console.log(num * 2)
console.log(num * 3) 
console.log(num * 4) 
console.log(num * 5)
console.log(num * 6) 
console.log(num * 7) 
console.log(num * 8)
console.log(num * 9) 

num = 2;
```
<br/>

**<u>여기서 잠깐!</u>**

변수를 선언하는 방법에는`var` , `let` , `const`   3가지가 있다.  

먼저 var는 변수를 선언하고, 선택적으로 초기화할 수 있다. ES5에서는 대표적인 변수로 사용되었지만 ES6부터는 `let` 과 `const` 가 많이 사용되었다. 그 이유는 호이스팅(Hoisting) 에 있다. 호이스팅이란 변수의 선언과 초기화를 분리한 후, 선언만 코드의 최상단으로 옮기는 것! 아래는 호이스팅의 예시이다. 사용은 위에서 하고있지만 선언은 아래에서 되고있다.   //*물론 let과 const도 호이스팅의 대상이긴 하지만 var와 달리 undefined로 초기화 하지 않는다.* 

```js
age = 6;
age++;
console.log(age);

var age;
```
<br/>

또한 변수의 중복 선언도 허용한다. 아래 예시를 보면 변수를 다른 값으로 중복 선언했지만 에러가 나지 않고 다른 값이 잘 출력되는 것을 볼 수 있다. 한마디로 재선언이 가능하여 코드량이 많아질 경우 파악이 힘들어 사용하기 어렵다. 이를 보완하기 위해 나온 것이 `let` 과 `const` 이다. 아래와 같은 코드를 출력했을 때 `let` 과 `const` 는 에러 메세지가 나온다. 

```js
var yourName = 'kanghyewon'
console.log(name) // kanghyewon
    
var yourName = 'wonhyekang'
console.log(name) // wonhyekang
```

<br/>

`let` 과 `const` 는 재선언이 불가능하다. 그렇다면 둘의 차이점은?

`let` 은 재선언은 불가능하지만 재할당은 가능하다. 그리고 `let`으로 선언한 변수는 자신을 선언한 블록과 모든 하위 블록을 스스로의 스코프로 가진다. 이게 무슨 말인가 싶다면 아래 두번째 코드를 보자. (스코프란 간단하게 말해서 변수에 접근할 수 있는 범위로 전역, 지역이 있다.)

```js
let yourName = 'kanghyewon'
console.log(name) // kanghyewon
    
let yourName = 'wonhyekang'
console.log(name) // 에러메세지-> 재선언 

yourName = 'wonhyekang'
console.log(name) //wonhyekang -> 재할당 
```
<br/>

```js
function letTest() {
  let x = 1;
  if (true) {
    let x = 2; // 다른 변수
    console.log(x); // 2
  }
  console.log(x); // 1
}
```


<br/>
그렇다면 `const` 는? 블록 범위의 상수를 선언한다. 상수의 값은 재할당할 수 없으며 다시 선언할 수도 없다. 


```js
const yourName = 'kanghyewon'
console.log(name) // kanghyewon
    
const yourName = 'wonhyekang'
console.log(name) // 에러메세지-> 재선언 

yourName = 'wonhyekang'
console.log(name) //에러메세지 -> 재할당 
```
<br/>


|                     |     재선언     |     재할당     |
| :-----------------: | :-----------: | :-----------: |
|  **var**            |       O       |       O       |
|  **let**            |       X       |       O       |
| **const**           |       X       |       X       |

<br/>
<br/>

**참고 사이트** 

- [변수 MDN](https://developer.mozilla.org/ko/docs/Learn/JavaScript/First_steps/Variables) 
- [변수의 선언 방식의 차이](https://velog.io/@bathingape/JavaScript-var-let-const-%EC%B0%A8%EC%9D%B4%EC%A0%90) 


<br/>

















