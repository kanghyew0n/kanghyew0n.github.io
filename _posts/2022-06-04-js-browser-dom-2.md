---
layout: single
title: "[JavaScript] 브라우저 DOM (2)"
categories:
  - DOM
tags:
  - DOM

---

### DOM 선택하기 

dom에 대해서 알아보다가 dom을 선택해서 특정 요소를 삭제하거나 텍스트를 변경하는데 궁금한 점이 생겼다. 바로 어떤건 ` getElementById()` 를 사용하기도 하고 다른건 ` getElementByClassName()`을 또 다른건 `querySelector()`을 사용한다는 점이다. 사실 앞에 두개는 ID, ClassName으로 찾는게 확실하게 알겠지만 Selector는 대체 어느 부분에서 적절하게 사용해야하는지 선택자에 대한 의문이 생겼다. 그래서 조금 더 알맞은 방법으로 코드를 짜고싶어서 알아보게 됐다. 

MDN에 검색해보면 선택자들이 굉장히 많이 나온다. (사진엔 `getElementById()` 는 없따! ) 각 전택자들이 어떤 것을 선택하고 언제 사용하면 좋을지 확인해보자!

![dom (1)](https://user-images.githubusercontent.com/104333249/172045781-2d489a27-e622-44d7-99ae-08c90cb3ab13.png)



### 1. Document.getElementById()

* 찾으려는 요소 ID. ID는 대소문자를 구분하는 문자열로, 문서 내에서 유일해야 한다.  즉, 하나의 값은 하나의 요소만 사용할 수 있다. 
* ID의 대소문자가 정확해야한다. 
* `Document.querySelector()`나 `Document.querySelectorAll()`과는 달리 `getElementById()`는 전역 `document` 객체의 메서드로만 사용할 수 있고, DOM의 다른 객체는 메서드로 가지고 있지 않다.

**HTML**

```html
<html>
<head>
  <title>getElementById 예제</title>
</head>
<body>
  <p id="para">어떤 글</p>
</body>
</html>
```

**JS**

```js
var elem = document.getElementById('para');
```


<br>
<br>





































