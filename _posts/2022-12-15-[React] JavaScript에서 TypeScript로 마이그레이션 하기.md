# 🚀 JavaScript에서 TypeScript로 마이그레이션 하기!

프로젝트로 진행한 Community 사이트의 배포를 heroku로 진행했었는데 유료 배포로 바뀌었다ㅜㅜ 그래서 새로 배포를 진행하게 되면서 javascript에서 typescript로 마이그레이션을 진행하려고 한다!
우선 가장 먼저 할 일! 패키지 설치를 해야한다. <br/>

[Community 깃허브 페이지 보러가 →](https://github.com/kanghyew0n/Toy-Community)

<br/>

## TypeScript 설치하기
```
npm install --save typescript @types/node @types/react @types/react-dom @types/jest
```

## tsconfig.json 설치하기
```
npx tsc --init
```

<br/>

## ⚠️ JS to TS (jsx to tsx) 에러 모음집
### 1. 컴포넌트 오류 
* [에러메세지] `'--jsx' 플래그를 제공하지 않으면 JSX를 사용할 수 없습니다.`
* [관련 링크](https://www.typescriptlang.org/ko/docs/handbook/jsx.html)

<img width="600" alt="스크린샷 2022-12-15 오전 12 22 32" src="https://user-images.githubusercontent.com/104333249/207636286-2e334a5c-ddeb-4685-911f-b04ec85565ae.png">

[해결 방법 1]
* `tsconfig.json 파일 "compilerOptions"`에  `"jsx": "react"` 추가
* 그리고 해당 컴포넌트 파일에 `import React from "react"` 추가
* react 모드의 출력 파일 확장자는 .js이다.

[해결 방법2]
* `tsconfig.json 파일 "compilerOptions"`에  `"jsx": "preserve"` 추가
* preserve 모드는 JSX를 출력 일부로 유지하여 이를 다른 변환 단계(Babel)에서 추가로 사용한다고 한다. 또한 출력 파일 확장자는 .jsx이다.

<br/>

### 2. null 개체
* [에러메세지] `개체가 'null'인 것 같습니다.`
* [해결 방법]  `tsconfig.json 파일 "compilerOptions"에 "strictNullChecks": false`
* 여러가지 해결 방법을 찾아보았으나,, 옵션을 추가하기로 결정!

<br/> 

### 3. event 타입 지정하기
* e.target.value를 사용할 일이 많은데 e의 타입을 지정해줘야 한다.
* 빠른 수정을 하게 될 경우 any타입으로 지정되기 때문에 따로 이벤트에 따라 따로 지정해주어야 한다.
<img width="817" alt="스크린샷 2022-12-15 오전 1 37 44" src="https://user-images.githubusercontent.com/104333249/207654461-24cecf20-fcf3-4df4-b05d-53c35a117ce4.png">

* 나같은 경우는 onChange 이벤트에 걸리는 fileUpload 함수에 e를 사용했기 때문에 `e: ChangeEvent<HTMLInputElement>` 이런식으로 타입을 지정해주었다. 
* 자신이 사용하고자 하는 이벤트에 마우스를 올리면 쉽게 확인할 수 있다!

<br/>
<br/>

뿌듯하구만! 



<br/>
<br/>

