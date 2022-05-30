---
layout: single
title: "[JavaScript] 비동기 (2)"
categories:
  - javascript
tags:
  - 자바스크립트  
  - 비동기 

---



### 비동기 이해하기 (2)



#### 목표 

- callback, Promise, async/await 구현 방법을 이해한다.
- Promise 실행 함수가 가지고 있는 두 개의 매개변수 `resolve` 와 `reject`를 활용할 수 있다.
- `new Promise()`를 통해 생성한 Promise 인스턴스가 사용할 수 있는 메서드의 용도를 이해한다.
- Promise의 세 가지 상태는 각각 무엇인지 설명할 수 있다.
- `async`/`await` 키워드와 함께 실행되는 함수는 어떤 타입이어야 하는지 이해한다.
- `await` 키워드를 사용할 경우 어떤 값이 리턴되는지 설명할 수 있다.







 #### Promise 실행 함수가 가지고 있는 두 개의 파라미터 resolve 와 reject 는 각각 무엇을 의미하나요?

실행 함수는 프로미스 구현에 의해 `resolve`와 `reject `함수를 받아 즉시 실행된다. `resolve` 및 `reject `함수는 호출할 때 각각 프로미스를 이행하거나 거부한다. 실행 함수는 보통 어떤 비동기 작업을 시작한 후 모든 작업을 끝내면 `resolve`를 호출해 프로미스를 이행하고, 오류가 발생한 경우 `reject`를 호출해 거부한다. 

* `resolve` : 작업을 성공적으로 끝낸 경우 그 결과를 나타내는 `value`와 함께 이행 
* `reject` : 오류 발생 시 에러 객체를 나타내는 `error`와 함께 호출해 거부함 



####  resolve, reject함수에는 전달인자를 넘길 수 있습니다. 이때 넘기는 전달인자는 어떻게 사용할 수 있나요?

* then() 메소드를 사용하여 resolve 함수에는 전달인자를 넘길 수 있음 

* catch() 메소드를 사용하여 reject 함수에는 전달인자를 넘길 수 있음 





####  new Promise()를 통해 생성한 Promise 인스턴스에는 어떤 메서드가 존재하나요? 각각은 어떤 용도인가요?





####  Promise.prototype.then 메서드는 무엇을 리턴하나요?

`then()` 메서드는 Promise를 리턴하고 두 개의 콜백 함수를 인수로 받는다. 

하나는 `Promise`가 **이행**했을 때 => `resolve`

다른 하나는 **거부**했을 때를 위한 콜백 함수이다.  => `reject`

```js
const promise1 = new Promise((resolve, reject) => {
  resolve('Success!');
});

promise1.then((value) => {
  console.log(value); // expected output: "Success!"
});
```



####  Promise.prototype.catch 메서드는 무엇을 리턴하나요?

`catch()`메서드는 `Promise` 거부된 사례만 반환하고 처리한다. 호출하는 것과 동일하게 동작합한다. 

```js
const promise1 = new Promise((resolve, reject) => {
  throw 'Uh-oh!';
});

promise1.catch((error) => {
  console.error(error); // expected output: Uh-oh!
});
```





####  Promise의 세 가지 상태는 각각 무엇이며, 어떤 의미를 가지나요?

- 대기 (*pending)* : 이행하지도, 거부하지도 않은 초기 상태

```js
new Promise((resolve, reject) => {});
```



- 이행 (*fulfilled)* : 연산이 성공적으로 완료됨

```js
function getNum(){
    return new Promise( (resolve, reject) => {
      let num = 50;
      resolve(num);
    })
  }
  
getData().then((resolveNum) => console.log(resolveNum));
```



- 거부 (*rejected)* : 연산이 실패함

```js
function getNum(){
    return new Promise( (resolve, reject) => {
      reject(new Error("에러"));
    })
  }
  
getNum().catch((error) => console.log(error));
```





####  await 키워드 다음에 등장하는 함수 실행은 어떤 타입을 리턴할 경우에만 의미가 있나요?





####  await 키워드를 사용할 경우, 어떤 값이 리턴되나요?





























