
<br/>

# [JavaScript] 문자열 

<br/>

## 문자열 변환 

여러가지 타입 문자열로 변환하기!

```js
String(123); //-> '123'
String(undefined); //-> 'undefined' 
String(null); //-> 'null'
String([1, 2, 3]); //-> '1, 2, 3'
String({}); //-> [object, Object]
String({name: 'kang'}); //-> [object, Object] : 객체가 온전하게 보여지지 않음 
```

 ```js
 JSON.stringify([1, 2, 3]); //-> '[1, 2, 3]'
 JSON.stringify({name: 'kang'}); //-> '{"name" : "kang"}'
 ```

```js
[1, 2, 3].toString(); //-> '1, 2, 3'
```

<br/>

문자열을 근본적으로 원시값처럼 변환할떄 사용 (밑에 코드 차이점 )

```js
String([1, 2, 3]); //-> '1, 2, 3'
JSON.stringify([1, 2, 3]); //-> '[1, 2, 3]'
```

<br/>

## 문자열 병합 

표현식 사용에서도 병합 가능함!

```js
function genHello(name) {
    const resultName = name || "이름없음";
    const resultName = name ? name : "이름없음";
    
    return "안녕하세요 " + resultName + "님 반갑습니다."
}

genHello('kang');
//-> '안녕하세요 kang님 반갑습니다.'
```

<br/>


## 문자열과 배열 (헷갈리는 부분!!!)

* 문자열에서 배열로 변환 : `.split()`

```js
'HELLO WORLD'.split('') //-> ['H', 'E', 'L', 'L', 'O', ' ', 'W', 'O', 'R', 'L', 'D']
'HELLO,WORLD'.split(',') //-> ['HELLO', 'WORLD']

```

<br/>

* 배열에서 문자열로 변환 1  : `.join()`

```js
['H', 'E', 'L', 'L', 'O', ' ', 'W', 'O', 'R', 'L', 'D'].join(); //-> 'HELLO WORLD'
```

<br/>

* 배열에서 문자열로 변환 2  : 전개연산자 

```js
const helloWorld = 'HELLO WORLD';

[...helloWorld]; //-> ['H', 'E', 'L', 'L', 'O', ' ', 'W', 'O', 'R', 'L', 'D']
```

<br/>

## 템플릿 리터럴 

* 멀티라인 (개행, 줄바꿈)이 자유로움 

* Basic String Formatting : 변수값이나 표현식을 문자열에 일부분으로 사용 가능함 
  * 보간법을 활용해서 표현식을 문자열로 포함 가능 

* HTML Escaping : 안전하게 사용하도록 도움 (XSS, SQL Injection)

<br/>

```js
function genHello(name) {
    return '안녕하세요' + name + '님 반갑습니다.'
}
//-> 이런 코드는 개행이 힘들고 injection(주입)이 취약함, 코드가 복잡해짐 
//-> return '안녕하세요\n' + name + '님 반갑습니다.' 이렇게 해야함 
```

<br/>

* 멀티라인 안전하게 사용하기 : 백틱 활용 

```js
function genHello(name) {
    return `안녕하세요 
    ${name} 님 
    반갑습니다.`
}

genHello('kang')
// '안녕하세요 
// kang님 
// 반갑습니다.'
```

<br/>

* DOM에 안전하게 삽입하기 

```js
const htmlTemplate = '<div>' + '안녕하세요' + '</div>';
body.innerHTML = htmlTemplate;
//-> 이런식으로 코드를 작성하면 해커들에게 취약한 문제점 발생 
```

```js
function genHello(innerText) {
    return `<div>${innerText}</div>`
}

const divTag = genHello('kang'); //-> '<div>kang</div>'
body.innerHTML = divTag; //-> DOM에 안전하게 삽입 가능 
```

<br/>
<br/>



