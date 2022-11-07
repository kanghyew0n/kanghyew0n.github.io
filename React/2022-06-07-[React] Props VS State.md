<br/>

# [React] Props VS State

<br/>


## Props VS State

* props 는 외부로 부터 전달받은 값 (이름, 성별)
* state  는 내부에서 변화하는 값 (나이, 거주지, 취업여부, 결혼/연애 여부)

<br/>

## Props 특징 

* 컴포넌트의 속성 (property) -> 성별이나 이름처럼 **변하지 않는** 외부로부터 전달받은 값, 애플리케이션에서 컴포넌트가 가진 속성에 해당함 
* 부모 컴포넌트로부터 전달받은 값 
* 어떠 타입의 값도 넣어 전달할 수 있도록 **객체 형태**이다.
* 읽기 전용이다 -> 변하지 않는 값이기 때문에 **읽기전용(read-only) 객체**이다.

<br/>

## Prop 사용하기 

1. 하위 컴포넌트에 전달하고자 하는 값(data)과 속성을 정의한다.
2. props를 이용하여 정의된 값과 속성을 전달한다.
3. 전달받은 props를 렌더링한다.

상위 컴포넌트와 하위 컴포넌트를 선언하고 상위 컴포넌트 안에 하위 컴포넌트를 작성한다.

```js
// 상위 컴포넌트 
function Parent() {
  return (
    <div className="parent">
      <h1>I'm the parent</h1>
      <Child />
    </div>
  );
};

// 하위 컴포넌트 
function Child() {
  return (
    <div className="child"></div>
  );
};
```

<br/>

React에서 속성 및 값을 할당하는 방법은  전달하고자 하는 값을`중괄호{}`를 이용하여 감싸준다. text라는 속성을 선언하고, 이 속성에 `"전달해!!!"`라는 문자열 값을 할당하여 `<Child>` 컴포넌트에 전달해 보자 

```js
<Child text={"전달해!!!"} />
```

<br/>

이제 `<Parent>` 컴포넌트에서 전달한 `"전달해!!!"`라는 문자열을 `<Child>` 컴포넌트에서 받아 보자. 함수에 인자를 전달하듯이 React 컴포넌트에 props를 전달하면 되고, 이 props가 필요한 모든 데이터를 가지고 오게 된다.

```js
function Child(props) {
  return (
    <div className="child"></div>
  );
};
```

<br/>

props를 렌더링하려면 JSX 안에 직접 불러서 사용하면 된다.  다만, props는 객체고, 이 객체의 `{ key : value }`는 `<Parent>` 컴포넌트에서 정의한 `{ attribute : value }`의 형태를 띠게 된다. 따라서 JavaScript에서 객체의 value에 접근할 때 dot notation을 사용하는 것과 동일하게 props의 value 또한 dot notation으로 접근할 수 있다. 아래와 같이 `props.text`를 JSX에 중괄호와 함께 작성하면 잘 작동한다.

```js
function Child(props) {
  return (
    <div className="child">
      <p>{props.text}</p>
    </div>
  );
}
```

<br/>

 `<Parent>` 컴포넌트의 `<h1>I'm the parent</h1>`를 `props`으로 불러올 수도 있지만  `<Parent>` 컴포넌트에서 `<Child text={"I'm the eldest child"} />` 처럼 직접 선언하고 불러올 수도 있다.

```js
function Parent() {
  return (
    <div className="parent">
      <h1>I'm the parent</h1>
      <Child text={"I'm the eldest child"} />
      <Child text={"I'm the second child"} />
      <Child />
    </div>
  );
}

function Child(props) {
  console.log("props : ", props); // props : Object
  return (
    <div className="child">
      <p>{props.text}</p>
    </div>
  );
}

export default Parent;

```

<br/>

props를 전달하는 방법으로 태그 사이에 value를 넣어 전달할 수 있다. `props.children`을 이용하면 해당 value에 접근하여 사용할 수 있다. 

```js
function Parent() {
  return (
    <div className="parent">
        <h1>I'm the parent</h1>
        <Child>I'm the eldest child</Child>
    </div>
  );
};

function Child(props) {
  return (
    <div className="child">
        <p>{props.children}</p>
    </div>
  );
};
```

<br/>

```js
const App = () => {
  const itemOne = "React를";
  const itemTwo = "배우고 있습니다.";

  return (
    <div className="App">
      {itemOne} {itemTwo}
      <Learn />
    </div>
  );
};

const Learn = (props) => {
  return <div className="Learn">
    <p>{props.children}</p>
  </div>;
};

export default App;

```

<br/>

## State

체크박스 구현 코드 

```js
import React, { useState } from "react";

function CheckboxExample() {
  const [isChecked, setIsChecked] = useState(false);

  const handleChecked = (event) => {
    setIsChecked(event.target.checked);
  };
  return (
    <div className="App">
      <input type="checkbox" checked={isChecked} onChange={handleChecked} />
      <span>{isChecked ? "Checked!!" : "Unchecked"}</span>
    </div>
  );
}

export default CheckboxExample;
```

<br/>

## State hook, useState

### useState 사용법

* `useState` 를 이용하기 위해서는 React로부터 `useState` 를 불러와야 한다. `import` 키워드로 `useState` 를 불러오자 

```js
import { useState } from "react";
```

* 이후 `useState` 를 컴포넌트 안에서 호출해준다. `useState` 를 호출한다는 것은 "state" 라는 변수를 선언하는 것과 같으며, 이 변수의 이름은 아무 이름으로 지어도 된다. 일반적인 변수는 함수가 끝날 때 사라지지만, state 변수는 React에 의해 함수가 끝나도 사라지지 않는다.
* 문법적으로 보면 아래 예시의 `isChecked`, `setIsChecked` 는 `useState` 의 리턴값을 구조 분해 할당한 변수이다.

```js
function CheckboxExample() {
// 새로운 state 변수를 선언하고, 여기서는 이것을 isChecked 라 부르겠습니다.
  const [isChecked, setIsChecked] = useState(false);
}
```

```js
function CheckboxExample() {
  // 1번 코드를 풀어쓰면
  const [isChecked, setIsChecked] = useState(false); // 1번

  //...

  // 2번 코드와 같습니다.
  const stateHookArray = useState(false); // 2번
  const isChecked = stateHookArray[0];
  const setIsChecked = stateHookArray[1];
}
```

<br/>

## 체크박스 

```js
import React, { useState } from "react";
import "./styles.css";

function CheckboxExample() {
  console.log("rerendered?");
  const [isChecked, setIsChecked] = useState(false);

  const handleChecked = (event) => {
    setIsChecked(event.target.checked);
  };

  return (
    <div className="App">
      <input type="checkbox" checked={isChecked} onChange={handleChecked} />
      <span>{isChecked ? "Checked!!" : "Unchecked"}</span>
    </div>
  );
}

export default CheckboxExample;

```

<br/>

## 입력창에 입력하면 그대로 반영 & 팝업창 뜨게하기 

```js
function NameForm() {
  const [name, setName] = useState("");

  const handleChange = (e) => {
    setName(e.target.value);
  };

  const handleClick = () => {
    alert(name);
  };
  return (
    <div className="App">
      <h1>Event handler practice</h1>
      <input type="text" value={name} onChange={handleChange}></input>
      <button onClick={handleClick}>Button</button>
      <button onClick={() => alert(name)}>Button</button>
      <h3>{name}</h3>
    </div>
  );
}
export default NameForm;

```

<br/>

## 드롭바 내용 선택하면 반영되게 하기 

```js
import React, { useState } from "react";
import "./styles.css";

function SelectExample() {
  const [choice, setChoice] = useState("apple");

  const fruits = ["apple", "orange", "pineapple", "strawberry", "grape"];
  const options = fruits.map((fruit) => {
    return <option value={fruit}>{fruit}</option>;
  });
  console.log(choice);
  const handleFruit = (event) => {
    //TODO : select tag 가 정상적으로 작동하도록 코드를 완성하세요.
    setChoice(event.target.value)
  };

  return (
    <div className="App">
      <select onChange={handleFruit}>{options}</select>
      <h3>You choose "{choice}"</h3>
    </div>
  );
}

export default SelectExample;

```


<br/>


## 상태에 따른 모달 창 

```js
vimport React, { useState } from "react";
import "./styles.css";

function App() {
  const [showPopup, setShowPopup] = useState(false);

  const togglePopup = () => {
    // Pop up 의 open/close 상태에 따라
    // 현재 state 가 업데이트 되도록 함수를 완성하세요.
    setShowPopup(!showPopup);
  };

  return (
    <div className="App">
      <h1>Fix me to open Pop Up</h1>
      {/* 버튼을 클릭했을 때 Pop up 의 open/close 가 작동하도록
          button tag를 완성하세요. */}
      <button className="open" onClick={togglePopup} >Open me</button>
      {showPopup ? (
        <div className="popup">
          <div className="popup_inner">
            <h2>Success!</h2>
            <button className="close" onClick={togglePopup}>
              Close me
            </button>
          </div>
        </div>
      ) : null}
    </div>
  );
}

export default App;

```

<br/>

## input 값 넣기 

```js
import "./styles.css";
import React, { useState } from "react";

export default function App() {
  const [username, setUsername] = useState("");
  const [msg, setMsg] = useState("");

  return (
    <div className="App">
      <div>{username}</div>
      <input
        type="text"
        value={username}
        onChange={(event) => setUsername(event.target.value)}
        placeholder="여기는 인풋입니다."
        className="tweetForm__input--username"
      ></input>
      <div>{msg}</div>
      {/* TODO : 위 input과 같이 입력에 따라서 msg state가 변할 수 있게 
      아래 textarea를 변경하세요. */}
      <textarea
        type="textarea"
        value={msg}
        onChange={(event) => setMsg(event.target.value)}
        placeholder="여기는 텍스트 영역입니다."
        className="tweetForm__input--message"
      ></textarea>
    </div>
  );
}

```

<br/>

```js
import React, { useState } from "react";

function SelectFruit() {
  const [choice, setChoice] = useState("apple");

  const fruits = ["apple", "orange", "pineapple", "strawberry", "grape"];
  const options = fruits.map((fruit, idx) => {
    return <option key={idx} value={fruit}>{fruit}</option>;
  });
  const handleFruit = (event) => {
		setChoice(event.target.value);
  };

  return (
    <div className="container">
      <select onChange={handleFruit}>{options}</select>
      <h3>You choose "{choice}"</h3>
    </div>
  );
}
```

<br/>

## 베어 미니멈 가능한 tweets.js

```js
import React, { useState } from "react";
import Footer from "../Footer";
import Tweet from "../Components/Tweet";
import "./Tweets.css";
import dummyTweets from "../static/dummyData";

const Tweets = () => {
  const [username, setName] = useState("");
  const [msg, setMsg] = useState("");

  // setNewData에 새로운 데이터 담아주기, 초기값은 dummyTweets
  const [newData, setNewData] = useState(dummyTweets);

  // setfiltername에 필터로 걸러진 이름들 담아주기
  const [filtername, setfiltername] = useState();

  // options에 username만 담은 데이터를 보관
  const options = newData.map((data) => {
    return <option value={data.username}>{data.username}</option>;
  });

  const tweet = {
    id: newData.length + 1,
    username: username,
    picture: dummyTweets[1].picture,
    content: msg,
    createdAt: new Date().toISOString(),
  };

  const handleButtonClick = (event) => {
    setNewData([tweet, ...newData]);
    // tweet 먼저 담아주고 다음 담겨있는 데이터 담아주기
    console.log(tweet);
    console.log(dummyTweets);
  };

  // filter함수 생성해서 setfiltername에 값 담아주기
  const filter = (event) => {
    setfiltername(event.target.value);
  };

  // input 창에 이름 입력하면 setName으로 받음
  const handleChangeUser = (event) => {
    console.log(username);
    setName(event.target.value);
  };

  // textarea 창에 내용 입력하면 setMsg로 받음
  const handleChangeMsg = (event) => {
    console.log(msg);
    setMsg(event.target.value);
  };

  return (
    <React.Fragment>
      <div className="tweetForm__container">
        <div className="tweetForm__wrapper">
          <div className="tweetForm__profile">
            <img src="https://randomuser.me/api/portraits/men/98.jpg" />
          </div>
          <div className="tweetForm__inputContainer">
            <div className="tweetForm__inputWrapper">
              <div className="tweetForm__input">
                <input
                  type="text"
                  //defaultValue="parkhacker"
                  placeholder="your username here.."
                  className="tweetForm__input--username"
                  value={username}
                  onChange={handleChangeUser}
                ></input>
                <textarea
                  //defaultValue="textarea"
                  placeholder="your content here.."
                  className="tweetForm__input--message"
                  value={msg}
                  onChange={handleChangeMsg}
                ></textarea>
              </div>
              <div className="tweetForm__count" role="status">
                <span className="tweetForm__count__text">
                  {"total: " + newData.length}
                </span>
              </div>
            </div>
            <div className="tweetForm__submit">
              <div className="tweetForm__submitIcon"></div>
              <button
                className="tweetForm__submitButton"
                onClick={handleButtonClick}
              >
                Tweet
              </button>
            </div>
          </div>
        </div>
      </div>
      <div className="tweet__selectUser">
        <select onChange={filter}>
          <option value="" selected>
            -- click ti filter tweets by username --
          </option>
          {options}
        </select>
      </div>
      {/*  map을 이용해서 Tweet 컴포넌트 불러주고 newData의 요소들을 ul에 담음 */}
      <ul className="tweets">
        {newData.map((ele) => (
          <Tweet key={ele.id} tweet={ele} />
        ))}
      </ul>
      <Footer />
    </React.Fragment>
  );
};
export default Tweets;

```






<br/>
<br/>