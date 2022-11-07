---
layout: single
title: "[JavaScript] 브라우저 DOM"
categories:
  - javascript
tags:
  - 자바스크립트  
  - DOM   
---

#### 시작하면서 

`HTML` (Hypertext Markup Language) 이란 웹사이트의 구조를 지정하는 기술적인 어어다. `HTML`을 작성할 때  요소를 작성하고 요소는 한 쌍의 태그로 감싸져있다.  예를들어 `input` 태그는 `<input type="text" name="name">` 이렇게 사용한다. 이를 브라우저에 띄우면 텍스트를 입력할 수 있는 창이 나오게 된다. 그렇다면 어떻게 저런 태그들이 브라우저에 텍스트 창으로 나타나게 될까?



### DOM 

`DOM` (Document Object Model) 은 `HTML` 또는 `XML` document와 상호작용 하고 표현하는 API 이다.  (위의 예시를 들어 설명하면 `HTML` 의 요소들을 가지고 실제 웹사이트처럼 구현해내는 것을 `DOM`이라고 간단하게 생각할 수 있다.) 

> HTML은 단순히 규칙에 따라 정해진 태그, 속성값으로 이루어진 언어이며,
> DOM은 브라우저가 HTML 파싱한 후 생성되는 객체 모델로, document에 접근가능한 API이다.

자바스크립트에서 DOM은 `document` 객체에 구현되어 있다. 브라우저에서 작동되는 자바스크립트 코드에서는, 어디에서나 `document` 객체를 조회할 수 있다. `DOM` 구조를 조회할 때에는 `console.dir` 이 유용하다.  `console.dir` 은 `console.log` 와 달리 DOM을 객체의 모습으로 출력한다. 

* 자바스크립트로 `DOM` 을 제어할 수 있다. (`DOM`은 자바스크립트 언어의 일부가 아님)

* `DOM`은 특정 프로그래밍 언어와 독립적으로 설계되어 있다. (모든 언어에서 빌드 가능)

* `DOM` 안에는 각종 `node` 들이 트리구조로 들어있다.  (`HTML` 의 요소는 `node` 라고 이해하기)

* `DOM` 구조를 조회할 때 `console.dir`  이 유용하다.

  

### DOM 객체의 CRUD

#### CREATE (생성)

새롭게 `div element` 를 생성하고 변수에 할당한다. 이때 변화가 없어 보이지만 현재 `div` 를 생성하고 DOM 트리에 연결을 안했기 때문에 그렇다. 이를 연결하기 위해 APPEND 해야한다. 

```js
document.createElement('div') 
const nameDiv = document.createElement('div') 
```



#### APPEND (연결)

`append`라는 메서드를 사용하여 변수를 `<body>` 에 넣어준다. `<div>` 요소에 아무 내용도 없어서 아무것도 보이지 않는다.

```js
document.body.append(nameDiv)
```



#### READ (조회, 찾기)

자바스크립트에서 원시자료형에서 변수의 값을 찾기 위해 변수 명을 조회하고, 참조 자료형에서 배열은 index를 객체는 key를 이용하여 값을 조회할 수 있다. 하지만 DOM으로 HTML 엘리먼트의 정보를 조회하기 위해서는 `querySelector` 의 첫번째 인자로 셀렉터(selector)를 전달하여 확인할 수 있다. 여러 개의 요소를 한 번에 가져오기 위해서는, `querySelectorAll` 을 사용한다. 

```js
const firstNameDiv = document.querySelector('.nameDiv') // 첫번째 element를 반환 
const nameDivs = document.querySelectorAll('.nameDiv') // 전달 선택자와 일치하는 모든 element 반환
```

이런 것도 있다고 알아만 두자 

```js
const 변수명1 = document.getElementById(container)
const 변수명2 = document.querySelector('#container')
console.log(변수명1 === 변수명2) // true
```



#### UPDATE (변경, 갱신, 수정)

 CREATE, APPEND, READ를 통해 새로운 DOM 객체를 만들고, 기존의 DOM 객체에 붙이고, DOM 객체를 선택해서 조회까지 했다. UPDATE는 `<div>` 태그를 업데이트 하여 내용을 입력한다.

* **textContnet**

```js
nameDiv.textContent = 'kanghyew0n';
console.log(oneDiv) // <div>kanghyew0n</div>
```

* **textContnet와 innerText의 차이점 **
  * `textContent`는 `script` 와 `style`  요소를 포함한 모든 요소의 콘텐츠를 가져오는 반면 `innerText`는 "사람이 읽을 수 있는" 요소만 처리함 
  * `textContent`는 노드의 모든 요소를 반환함, 그에 비해 `innerText`는 스타일링을 고려하며, "숨겨진" 요소의 텍스트는 반환하지 않음 (display: none)

* **textContnet와 innerHTML의 차이점 **
  * ` innerHTML`을 사용해 요소의 텍스트를 가져오거나 쓰는 경우가 있지만, HTML로 분석할 필요가 없다는 점에서 `textContent`의 성능이 더 좋다. 
  * `textContent`는 XSS 공격 (en-US)의 위험이 없다. (XSS(교차 사이트 스크립팅)는 공격자가 웹 사이트에 악성 클라이언트 측 코드를 삽입할 수 있도록 하는 보안 악용이다.)

* **setAttribute / removeAttribute**

요소의 속성값을 정한다. 밑에 예시에서는 `nameDiv` 의 `id` 를 `myName` 으로 정해준다. 

```js
element.setAttribute('attributename', 'attributevalue')
element.removeAttribute(attributename)

nameDiv.setAttribute('id', 'myName') // id="myName"
```

* **classList**

`classList.add`를 이용하여 클래스를 추가한다.  

```js
nameDiv.classList.add('nameDiv');	// class="nameDiv"
console.log(nameDiv) // <div class="nameDiv">kanghyew0n</div>
```



#### DELETE (삭제)

* 삭제하려는 요소의 위치를 알고 있는 경우에 `remove` 메서드를 사용하여 삭제한다. 

```js
const container = document.querySelector('#container')
const nameDiv = document.createElement('div')
container.append(nameDiv)
nameDiv.remove() // append 했던 요소를 삭제할 수 있음 
```

* 컨테이너의 모든 자식요소를 제거하려면 

```js
document.querySelector('#container').innerHTML = '';
```

* `removeChild` 는 자식 요소를 지정해서 삭제하는 메서드이다. 모든 자식 요소를 삭제하기 위해, 반복문(while, for, etc.)을 활용할 수 있다. 다음의 코드는 자식 요소가 남아있지 않을 때까지, 첫 번째 자식 요소를 삭제하는 코드이다. container의 첫 번째 자식 요소가 존재하면, 첫 번째 자식 요소를 제거한다. 

```js
const container = document.querySelector('#container');
while (container.firstChild) {
  container.removeChild(container.firstChild);
}
```

* 클래스 명이 같은 모든 요소를 삭제하기 위해서는 `querySelectorAll` 로 모든 요소를 선택하여 `nameDivs` 에 담아주고  클래스 이름이 nameDiv 인 요소만 찾아 제거한다.

```js
const nameDivs = document.querySelectorAll('.nameDiv');
nameDivs.forEach((nameDiv) => nameDiv.remove());
```

 













