<br/>

# [JavaScript] 객체

<br/>

### 객체 

객체는 키와 값 쌍(key-value pair)으로 이루어져 있다.

`name`, `age`, `email`, `add`는 키 / `kanghyewon`,  `24`,`abc@abc.com`, `korea` 는 값이다.

```js
let user = {
	name:'kanghyewon',
	age: '24',
	email: 'abc@abc.com',
	add: 'korea'
};
```

<br/>

객체는 두 가지 방법으로 사용된다.

**방법1: Dot notation**

```js
user.name; // 'kanghyewon'
user.age; // '24'
```

<br/>

**방법2: Bracket notation** : 문자열로 들어감!

key 값이 변수일 때 (동적일 때) 이 방법을 사용해야됨 -> 예를 들어 함수 안에 매개변수로 들어갈 때는 key의 값이 바뀔 수 있기 때문에 브라켓 방법으로 사용해야함 

```js
user['name']; // 'kanghyewon'
user['age']; // '24'
```

```js
let keyName = 'name';
user[keyName]; // 'kanghyewon'
```

```js
let person = {
	name: 'hyewon',
	age: '24'
};

function getProperty(obj, propertyName) {
	return obj[propertyName]; // obj['name']
}

let output = getProperty(person, 'name');
console.log(output); // 'hyewon'
```

위의 코드에서 `propertyName`이라는 변수의 키 값이 변하기 때문에  Bracket notation을 사용해야 한다.

<br/>

**키워드 추가 **

```js
let person = {
	name: 'hyewon',
	age: '24'
};

person['add'] = '안양';
person.tag = ['#안녕', '#하세요'];
```

<br/>

**키워드 삭제**

```js
let person = {
	name: 'hyewon',
	age: '24',
	add: '안양',
	tag: '#안녕', '#하세요'
};

delete person.add;
```

<br/>

**in 연산자 **

해당하는 키가 있는지 확인할 수 있다.

```js
let person = {
	name: 'hyewon',
	age: '24'
};

'name' in person; //true
'add' in person; //false
```

<br/>
<br/>
