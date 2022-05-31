---
layout: single
title: "[JavaScript] 비동기 (1)"
categories:
  - javascript
tags:
  - 자바스크립트  
  - 비동기 

---

### 비동기 이해하기 (1)



#### callback review

* 다른 함수 A의 전달인자로 넘겨주는 함수 B
* parameter를 넘겨 받는 함수 A는 callback 함수 B를 필요에 따라 즉시 실행(Synchronously) 할 수도 있고,
* 아니면 나중에 (asynchronously) 실행할 수도 있다.

```js
function B () {
    console.log('called at the back!');
}

function A(callback) {
    callback(); //callback === B
}

A(B);
```



* callback in action: 반복 실행하는 함수 (iterator)

```js
let arr = [2, 4, 6];
arr.map(function(ele, idx) {
    return ele * ele;
}); //-> 배열의 길이만큼 반복함 
```



* callback in action : 이벤트에 따른 함수 (event handler)

```js
document.querySelector('#btn').addEventListener('click', function(e){
    console.log('button clicked');
})
```



**헷갈리지 말기 !**

함수 실행을 연결하는 것이 아닌 함수 자체를 연결해야함!

```js
function handleClick () {
    console.log('button clicked');
}

document.querySelector('#btn').onclick = handleClick;// (O)
document.querySelector('#btn').onclick = function(){
    handleClick();
};// (O)
document.querySelector('#btn').onclick = handleClick.bind();// (O)
document.querySelector('#btn').onclick = handleClick(); // (X)
```



#### blocking VS non-blocking

* `blocking` : 요청 작업이 끝날때까지 다른 작업을 하지 않고 기다림 
* `non-blocking` : 요청 작업이 수행하는 동안 다른 작업도 수행 가능 



#### 동기(synchronously) VS 비동기 (asynchronously)
처음 접하는 개념이라서 이름부터 낯설지만 sync는 눈에 많이 익숙하다,,, 우선! 개념을 이해하는 것은 어렵지 않다!

* 동기 (`synchronously`) : 동기식이란 각 당사자가 즉시 메시지를 수신하는 실시간 통신을 말한다 ([MDN](https://developer.mozilla.org/en-US/docs/Glossary/Synchronous))
* 비동기 (`asynchronously`) : 비동기란 동시에 발생하는 둘 이상의 개체 또는 이벤트 (또는 이전 항목이 완료될 때까지 기다리지 않고 발생하는 여러 관련 작업)를 나타낸다 ([MDN](https://developer.mozilla.org/en-US/docs/Glossary/Asynchronous))

카페에서 아르바이트 한 경험을 떠올려보면 혼자 아르바이트 하는 경우를 동기적이라고 할 수 있을 것 같다. 1. 주문을 받고  2. 음료를 만들고  3. 손님께 음료를 드리고 그 다음 1. 주문을 받고  2. 음료를 만들고  3. 손님께 음료를 드리고 .... 순서대로 하나의 동작이 끝나면 그 다음 과정을 할 수 있었다.  (순차적으로) 

하지만 여러명이 함께 아르바이트를 하는 경우를 비동기적이라고 할 수 있을 것 같다. 한명은 1-1. 주문을 받고 한명은 1-2. 음료를 만들고  한명은  1-3. 음료를 드리고  또 다시 2-1. 주문을 받고 한명은 2-2. 음료를 만들고  한명은  2-3. 음료를 드리고  ..... 1번 과정을 동시에, 2번 과정을 동시에 할 수가 있다. 

아래 코드를 보면 이해가 조금(?) 더 간다.



* 동기적 

```js 
function firstFunc() {
    console.log('첫번째 실행');
    SecondFunc();
}

function SecondFunc(){
    console.log('두번째 실행');
    thirdFunc();
}

function thirdFunc() {
    console.log('세번째 실행');
}

firstFunc(); // 첫번째 실행 -> 두번째 실행 -> 세번째 실행
// 순차적으로 실행 됨 
```

<br/>

* 비동기적 

```js
function firstFunc(){
    console.log('첫번째 실행');
    func2();
}

function SecondFunc(){
    setTimeout(function(){
        console.log('1초 뒤에 실행되겠다!');
    }, 1000);
    func3();
}

function thirdFunc(){
    console.log('몇번째 실행?');
}
func1(); // 첫번째 실행 -> 몇번째 실행? -> (1초 뒤) -> 1초 뒤에 실행되겠다!
// 비동기적으로 실행 됨 
```

<br/>

**잠깐, 갑자기 `setTimeout` ?**

`setTimeout()`은 만료된 후 함수나 지정한 코드 조각을 실행하는 타이머를 설정한다. 위에 코드에서는 1000ms 뒤에 지정한 함수를 실행한다. ('1초 뒤에 실행되겠다!') 

`setTimeout()`은 비동기 함수로서, 함수 스택의 다른 함수 호출을 막지 않는다. 달리 말하자면, `setTimeout()`을 사용해서 다음 함수 호출을 "일시정지" 할 수는 없다. 


<br/>
#### 그렇다면 blocking VS non-blocking / sync VS async 같은 개념일까?

아니다! 서로 관점의 차이가 있다.















