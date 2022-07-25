---
layout: single
title: "[시작하기] 설치를 어떻게 했더라 ..."
categories:
  - 시작하기 
tags:
  - 리액트   
  - styled-component
  - storybook 
  

---

<br/>
<br/>


# React 시작하기 

1. `node` 와 `npm` 이 설치되어있는지 확인한다 (생략 가능) 

``` js
// node와 npm 버전정보가 나오면 설치 되어있는 것 

$ node --version
$ npm --version
```

2.  이동하고싶은 디렉토리로 이동하기 

```js
$ cd Desktop
$ mkdir 원하는 폴더명(생략 가능)
```

3. 리액트 시작하기 

```js
$ npx create-react-app 폴더명 
// 예시) npx create-react-app react-crud-project
```

4. 리액트 실행하기 

```js 
cd 폴더명
$ code .

// 원하는 에디터에서 터미널 열기 
$ npm install (npm i)
$ npm start
```

<br/>
<br/>


## React Router 시작하기 

* 리액트 프로젝트를 생성했다면 해당 프로젝트를 에디터로 켜줌 

```js
// 해당 디렉토리가 실행되고 있는 에디터 터미널에서 진행 (혹은 터미널에서 해당 폴더로 이동)
$ npm install react-router-dom@^6.3.0 // (원하는 버전)
```

- `package.json` 파일에 들어가서 `"react-router-dom": "^6.3.0"` 있나 확인 

```js 
// router를 사용할 폴더에 
import React from 'react'
import { BrowserRouter, Routes, Route, Link } from "react-router-dom"; 
// 이 구문 넣어주기 
```

* `<BrowserRouter>` 컴포넌트는 상위에 작성되어 있어야 React Router의 컴포넌트들을 사용가능 (사용 예시)

```js
function App() {
  return (
    <BrowserRouter>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/mypage">MyPage</Link>
            </li>
            <li>
              <Link to="/dashboard">Dashboard</Link>
            </li>
          </ul>
        </nav>

         <Routes>
          <Route path="/" element={<Home />} /> 
			{/* 경로는 path로 컴포넌트는 element로 연결해 줍니다. */}
          <Route path="/mypage" element={<MyPage />} /> 
          <Route path="/dashboard" element={<Dashboard />} />
        </Routes>
      </div>
    </BrowserRouter>
  );
}
```

<br/>
<br/>



## 서버 실행하기 

* `node` 로 실행하기 

```js
$ node 파일_경로 
// 예시) node server.js
```

* `nodemon`으로 실행하기 

```js
$ npx nodemon 파일_경로 
// 예시) npx nodemon server.js
```

* +express 설치하기 

```js
$ npm install express
```


<br/>
<br/>


## Styled Components 설치하기

1. 라이브러리 설치하기 

```js
# with npm
$ npm install --save styled-components

# with yarn
$ yarn add styled-components
```

2. `package.json` 에 코드 추가하기  -> 여러 버전의 Styled Components가 설치되어 발생하는 문제를 줄임

```js
{
  "resolutions": {
    "styled-components": "^5"
  }
}
```

3. `import` 해주기 

```js
// Styled Components 사용할 파일로 불러오기 
import styled from "styled-components"
```

<br/>


 #### +전역 스타일 설정하기

*  전역 스타일을 설정하기 위해 Styled Components에서 `createGlobalStyle` 함수 불러오기 

 ```js
 import { createGlobalStyle } from "styled-components";
 ```

* 작성 예시 

```js
const GlobalStyle = createGlobalStyle`
	button {
		padding : 5px;
    margin : 2px;
    border-radius : 5px;
	}
```

```js
function App() {
	return (
		<>
			<GlobalStyle />
			<Button>전역 스타일 적용하기</Button>
		</>
	);
}
```


<br/>
<br/>


## Storybook 사용하기 

리액트 프로젝트 만든 후 

* storybok 설치하기 

```js
$ npx storybook init
```

> Storybook 설치 완료 ->  `/.storybook` 폴더 & `/src/stories` 폴더 생성,  `/.storybook` 폴더에는 Storybook 관련 설정 파일이, `/src/stories` 폴더에는 Storybook 예시 파일들이 들어있다.

* Storybook 실행

```js
$ npm run storybook
```

>  /.storybook 안에 있는 Storybook 설정 파일에 의해서 컴포넌트 파일과 똑같은 파일 이름에 .stories를 붙여 파일을 만들면 알아서 스토리로 인식함 


<br/>
<br/>


## 미디어 쿼리 적용하기 (반응형)

- 스마트폰, 테블릿과 같은 모바일 장치 전용 설정
- 모바일 장치의 화면 크기에 따라 페이지를 출력하려면 반드시 사용해야 하는 설정 

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

* initial-scale=1.0 : 첫 페이지 로딩 시 확대 / 축소가 되지 않은 원래 크기를 사용하도록 함
* viewport : 웹페이지가 사용자에게 보여지는 영역

> viewport를 설정하지 않았을 경우! viewport의 크기가 줄어들 경우 웹페이지를 스크롤 해야 볼 수 있거나 폰트 사이즈나 이미지의 scale이 과하게 줄어든다.

```css
/*css 파일 혹은 태그 안에서 미디어 쿼리 작성하기 */

@media 미디어 타입 (조건(너비 및 높이)) {
    (CSS 입력하는 부분)
}

/*예제*/
@media screen (max-width: 400px) {
    body {
			color: red;
		}
}

/*논리곱(and) 미디어 쿼리도 가능 (둘 다 만족했을 때)*/
@media screen and (min-width: 400px) and (orientation: landscape) {
    body {
        color: blue;
    }
}

/*논리합(or) 미디어 쿼리도 가능 (둘 중 하나 만족했을 때)*/
@media screen and (min-width: 600px), screen and (orientation: landscape) {
    body {
        color: blue;
    }
}

/*부정(not) 미디어 쿼리*/
@media not all and (orientation: landscape) {
    body {
        color: blue;
    }
}
```


<br/>
<br/>


## @keyframes 사용하기 (CSS 애니메이션 )

* 키 프레임 블록 생성하기 

```css
/* '%' 단위로 시간 진행에 따른 상태를 작성하기 */

@keyframes 애니메이션이름 {
	0% {            /* from 이라고 작성가능*/
		CSS속성 : 속성값; 
	}

	50% {           /* 애니메이션 진행도에 따른 스타일을 설정하기*/
                  /* 필요하다면 1부터 99까지도, 소수점까지도 모두 작성가능 .*/
		CSS속성 : 속성값;
	}

	100% {          /* to 라고 작성 가능.*/
		CSS속성 : 속성값;
	}
}

/*예시*/
@keyframes lotate {
	0% {
		transform : rotate(0deg)
	}

	50% {
		transform : rotate(180deg)
	}

	100% {
		transform : rotate(360deg)
	}
}

/* 시작 시점에선 0도, 50% 시점에선 180도, 완료 시점에선 360도 회전시키는 애니메이션*/
```


<br/>
<br/>


## Canvas 사용하기 

* DOM에서 불러올 canvas 태그 작성하기 

```html
<canvas id="canvas">
	캔버스를 지원하지 않는 브라우저에서는 캔버스 대신 태그 사이 내용이 표시됨
</canvas>
```

* js에서 엘리먼트 선택해주기 

```js
const canvas = document.querySelector("#canvas");
```

* 캔버스 요소의 `width`, `height` 속성은 픽셀 단위로만 명시해야 인식하도록 되어 있음 

```html
<canvas id="canvas" width="500" height="500"></canvas>
		// 500픽셀 * 500픽셀로 설정됨 

<canvas id="canvas" width="50vw" height="40vh"></canvas>
		// vw, vh를 전달했지만 50픽셀 * 40픽셀로 설정됨 

```

* [MDN 기본 사용법  링크](https://developer.mozilla.org/ko/docs/Web/API/Canvas_API/Tutorial/Basic_usage) 

* [캔버스 튜토리얼 MDN 링크](https://developer.mozilla.org/ko/docs/Web/API/Canvas_API/Tutorial)



<br/>
<br/>

























