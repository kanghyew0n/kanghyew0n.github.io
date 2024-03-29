<br/>

# [JavaScript] 객체지향 프로그래밍 

<br/>




## 클래스(Class)와 인스턴스(Instance) 

`Class` 는 객체를 생성하기 위한 템플릿이다. 클래스는 데이터와 이를 조작하는 코드를 하나로 추상화한다. 자바스크립트에서 클래스는 프로토타입을 이용해서 만들어졌지만 ES5의 클래스 의미와는 다른 문법과 의미를 가진다. (MDN)

`Instance` 는 템플릿을 바탕으로 한 객체이다. 개체는 일반 함수를 정의하듯 만들지만 함수를 이용하는 방법이 다르다.


<br/>


## 클래스(Class)를 만드는 방법 

1. `ES5` (클래스 표현식) : 함수를 사용하는 방법 

* Class 표현식을 이름을 가질 수도 있고, 갖지 않을 수도 있다.

```js
let Rectangle = class { // unnamed
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);//"Rectangle"

let Rectangle = class Rectangle2 { // named
  constructor(height, width, color) {
    this.height = height;
    this.width = width;
    this.color = color;
  }
};
console.log(Rectangle.name); //"Rectangle2"
```



2. `ES6` (클래스 선언) : 클래스 생성자를 이용하는 방법 

* `class` 키워드를 사용해야한다 -> 클래스 안에는 생성자(constructor) 가 있음 

* 자바스크립트는 클래스의 새로운 인스턴스를 만들 때 생성자 메소드를 호출한다.

```js
class Rectangle { //class 키워드 사용 
  constructor(height, width, color) {
    this.height = height;
    this.width = width;
    this.color = color;
  }
}
```


<br/>


## 인스턴스(Instance)를 만드는 방법 

* `new` 키워드를 사용한다. (`new` + 클래스 명)
* 생성된 인스턴스 객체 (`redRectangle` , `blueRectangle`) 는 class의 고유한 속성&메소드 가짐 

```js
let redRectangle = new Rectangle(3, 4, '레드');
let blueRectangle = new Rectangle(6, 10, '블루');
```


<br/>


## this?

* `this`는 인스턴스 객체를 의미한다. parameter로 넘어온 넓이, 높이, 색상 등은 인스턴스 생성 시 지정하는 값이며,  위와 같이 this에 할당한다는 것은 만들어진 인스턴스에 해당 넓이, 높이, 색상을 부여하겠다는 의미이다. 



- 클래스
- 인스턴스
- new 키워드
- 생성자 함수
- ES5 클래스 작성 문법
- ES6 클래스 작성 문법


<br/>


### 객체지향 프로그래밍 (OOP: Object Oriented programming)

`객체 지향 프로그래밍`은 프로그램 설계 방법론의 일종으로 *절차 지향 프로그래밍과 다르게 데이터의 접근과 처리 과정에 대한 모형(객체)을 만들어내는 방식이다.

(*절차지향 프로그래밍 : 프로세스가 함수 단위로 순서대로(절차적으로) 진행되는 것 -> 기능 중심)

* 객체 내에는 "데이터와 기능이 함께 있다"라는 원칙에 따라 메서드와 속성이 존재한다.
* OOP는 절차지향에 비해서 사람의 사고방식과 더 가까움 (사람이 **세계를 보고 이해하는 방법**을 흉내 낸 방법론)
* 객체들 간의 유기적인 상호작용(객체 단위)을 통해 프로세스 진행 -> 객체 중심 



<br/>

## OOP의 기본 개념 

객체지향 프로그래밍의 장점을 말하기 위해 필요한 주요 개념 4가지가 있다. 

* `캡슐화` (Encapsulation)
* `추상화` (Abstraction)
* `상속` (Inheritance)
* `다형성` (Polymorphism)



<br/>

## 캡슐화 (Encapsulation)

- 객체의 속성(data fields)과 행위(메서드, methods)를 하나로 묶고
- 실제 구현 내용 일부를 내부에 감추어 은닉함 -> 정보은닉의 특징
- 느슨한 결합(Loose Coupling)에 유리: 언제든 구현을 수정할 수 있음 -> **재사용성 높임 **


<br/>


## 추상화  (Abstraction)

* 복잡한 자료, 모듈, 시스템 등 특정한 대상을 관찰하여 핵심적이고 특징적인 공통점(개념 혹은 기능)들을 뽑아내는 과정 -> 인터페이스 단순해짐 
*  **코드가 복잡하지 않게 만들고, 단순화된 사용으로 변화에 대한 영향을 최소화함 **


<br/>


## 상속 (Inheritance)

* 기본 클래스(base class)의 특징을 파생 클래스(derived class)가 상속받음 -> 편의상 부모/자식관계 
* 기존 클래스에 기능을 가져와 재사용할 수 있으면서도 동시에 새롭게 만든 클래스에 새로운 기능을 추가할 수 있음 -> 계층형 구조가 형성됨 & **불필요한 코드 줄여 재사용성 높임**
* 계층형 구조의 형태에서 아래로 내려갈수록 구체화되고 위로 갈수록 일반화 된다고 표현함 



## 다형성 (Polymorphism)

* 다양한 형태가 존재한다는 뜻 -> 같은 동작이지만 다른 결과물이 나오는 것 
* 같은 이름의 속성을 유지하여 메서드 이름을 낭비하지 않는다는 것
* 같은 동작이라도 여러가지 형태가 존재한다면 if문이 반복적으로 돌아 구분을 해야하지만 그럴 필요가 없어짐 -> **동일한 메서드에 대해 객체의 특성에 맞게 달리 작성하는 것 가능**



<br/>

## 프로토타입 (Prototype)

JavaScript는 흔히 **프로토타입 기반 언어(prototype-based language)**라 불린다. 모든 객체들이 메소드와 속성들을 상속 받기 위한 템플릿으로써 **프로토타입 객체(prototype object)**를 가진다는 의미이다. (MDN)



* 상위 프로토타입 객체로부터 메소드와 속성을 상속 

```js
function Person() {
    this.name = 'name';
    this.age = 'age';
}

let hyewon = new Person();
console.log(hyewon); // {name: 'name', age: 'age'}

//Person -> hyewon 에게 name, age 물려줌 
```



* `prototype`을 사용하면?

```js
function Person() {
    this.name = 'name';
    this.age = 'age';
} // -> 여기에 직접 입력하면 hyewon도 직접 가짐 

Person.prototype.gender = 'gender'; //-> 여기에 쓰면 Person만 가짐 

let hyewon = new Person()
console.log(hyewon.gender); // gender
console.log(hyewon) // {name: 'name', age: 'age'}
```

![image-20220525172637457](https://user-images.githubusercontent.com/104333249/172045964-3dc86b60-afe3-411c-859c-185c341cfae6.png)

-> gender는 Person의 프포토타입에 보관되어있음 


```js
hyewon.gender; 

// gender 를 가져오는 방법 
// 1. hyewon 이  gender를 가지고 있나? 
// 2. 아니, hyewon의 프로토타입 객체 (Person() 생성자의 프로토타입)에 gender 가 있니?
// 3. 있음, 그렇다면 Person.prototype에서 gender를 가져옴 
```



```js 
function Person() {
    this.name = 'name';
    this.age = 'age';
}

let hyewon = new Person();
hyewon.valueOf();

// 우리가 valueOf()를 추가해준 적이 없음 
// 어떻게 사용 가능할까?
// valueOf()를 가져오는 방법 
// 1. hyewon 이 valueOf()를 가지고 있나? 
// 2. 아니, hyewon 프로토타입 객체 (Person() 생성자의 프로토타입)에 valueOf() 가 있니?
// 3. 아니, 그렇다면 Person() 생성자의 프로토타입 객체의 프로토타입 객체(Object() 생성자의 프로토타입) 가 valueOf() 를 가지고있니?
// 가지고있다! 여기에서 호출함 
// 이 과정을 프로토타입 체인(prototype chain)이라 부르며
```

* 3. 은 여기서 찾아낸 후 호출!
![image-20220525175558294](https://user-images.githubusercontent.com/104333249/172045978-1df9814f-2e2d-4de6-8120-f3d1b58c8c71.png)




<br/>



## 프로토타입 체인 (Prototype Chain)

상속 관점에서 자바스크립트의 생성자는 객체이다. 이 객체들은 프로토타입 속성을 가지는데 자신의 `프로토타입`이 되는 다른 객체를 가리킨다. 그 객체의 프로토타입 또한 프로토타입을 가지고 있고 이것이 반복된다 -> `프로토타입 체인`

결국 `null`을 프로토타입으로 가지는 오브젝트에서 끝난다. null은 더 이상의 프로토타입이 없다고 정의되며, `프로토타입 체인`의 종점 역할을 한다. (MDN)



#### `extends` 와 `super` 키워드를 이용해서 상속 구현하기 

* `extends` : **extends** 키워드는 클래스를 다른 클래스의 자식으로 만들기 위해 class 선언에 사용된다.

* `super` : **super** 키워드는 부모 오브젝트의 함수를 호출할 때 사용된다.

* 주의 )  파생 클래스에서 super() 함수가 먼저 호출되어야 `this` 키워드를 사용할 수 있다. 그렇지 않을 경우 참조오류 발생 


```js 
//부모 클래스 Polygon
class Polygon {
    constructor(height, width){
        this.name = 'Polygon';
        this.height = height;
        this.width = width;
    }

    sayName() {
    	console.log('Hi, I am a ', this.name + '.');
  }
}

//부모 클래스 Polygon -> 자식 클래스 Square
class Square extends Polygon {
    constructor(length){
    	//super키워드를 통해 부모 클래스 생성자 호출
        //super키워드가 먼저 호출되기 전 this가 나오면 참조오류 발생 
        // Polygon의 길이와 높이를 넘겨줍니다.
        super(height, width);
        
        //추가 프로퍼티 초기화
        this.length = 'length';
    }

    get area() {
     return this.height * this.width;
  }

    set area(value) {
      this.area = value;
  }
}
```


<br/>

## DOM과 프로토타입

* div 엘리먼트의 상속 관계 :`HTMLDivElement` -> `HTMLElement` -> `Element` -> `Node` -> `EventTarget`
* `EventTarget`의 부모로는 모든 클래스의 조상인 `Object`가 있음 

* 이것을 바탕으로 아래의 답을 알아낼 수 있따.

```js 
let div = document.createElement('div');

div.__proto__.__proto__ //HTMLElement
div.__proto__.__proto__.__proto__ //Element
```



* 프로토타입 체인의 과정 

```js
let div = document.createElement('div');

div.__proto__ 
div.__proto__.__proto__
div.__proto__.__proto__.__proto__
div.__proto__.__proto__.__proto__.__proto__
div.__proto__.__proto__.__proto__.__proto__.__proto__
div.__proto__.__proto__.__proto__.__proto__.__proto__.__proto__
div.__proto__.__proto__.__proto__.__proto__.__proto__.__proto__.__proto__
```

![image-20220526111738443](https://user-images.githubusercontent.com/104333249/172045990-49d8ab6f-a14c-4e6a-a78b-857169a565fe.png)




- 프로토타입 체인
- .prototype
- `.__proto__`
- Object



<br/>
<br/>

