# Bundle 파일 분석을 해보쟈
개발자 도구 Performance탭에서 보면 아래 사진처럼 chunk 파일에 시간이 오래 소요되는 것을 확인할 수 있다. 이것들이 다운받아져야 다른 js 파일들이 로드되기 때문에 화면에 요소가 나오는 시간에 영향을 미친다.
그렇다면 저 파일은 왜 저렇게 시간이 오래 걸릴까? <br/>

<img width="1149" alt="스크린샷 2023-01-08 오후 10 48 57" src="https://user-images.githubusercontent.com/104333249/211199593-49a943e9-7983-4098-bd42-06214f3810aa.png">

# cra-bundle-analyzer
`webpack-bundle-analyzer`은 웹팩 출력 파일의 크기를 시각화해주는 라이브러리다. 하지만 cra로 리액트를 시작한 코드를 분석할 수가 없다. (cra 제공 webpack을 사용하기 때문). 
따라서 cra-bundle-analyzer를 사용하면 같은 기능을 사용할 수 있도록 도와준다. <br/>

<br/>

**→ 설치**
```
npm i cra-bundle-analyzer
```
**→ 사용**
```
npx cra-bundle-analyzer
```

<br/>


![스크린샷 2023-01-08 오후 10 54 16](https://user-images.githubusercontent.com/104333249/211199927-63558d3d-2cb4-489e-8f1b-f027fa397948.png)

실행시켜보면 이런 화면이 나오는데 chunk.js 파일이 크게 자리잡고 있는것을 볼 수 있다. chunk 파일은 src를 가지고 있으며, 모듈에서 리액트 돔을 제외하고 refractor 이라는 것이 절반을 차지하고 있다. <br/>


<img width="829" alt="스크린샷 2023-01-08 오후 10 56 18" src="https://user-images.githubusercontent.com/104333249/211200038-9b94bfb5-0e71-47fa-b3e5-c49419d6334e.png">

이것은 코드블럭에서 사용하는 highlighter인데 이것은 게시글 디테일 부분에서만 사용하는 라이브러리이다. 하지만 이것을 페이지 로딩부터 다운받기 때문에 성능이 떨어지게 되는것이다. (초기 로딩속도에서 오래걸림)
따라서 이것을 코드 분리를 통해 해결할 수 있다!

<br/>

# Code Splitting & Lazy Loading
Code Splitting ? 코드를 분할하는 것으로 덩치가 큰 번들 파일을 작은 사이즈 파일로 만드는 것을 의미한다. <br/>
방식으로는 페이지 별로 코드를 분할하는 방법과 모듈별로 코드를 분할하는 방법, 이 둘을 혼용하여 사용하는 방법이 있다. 여기서 포인트는! 
`불필요한 코드또는 중복되는 코드 없이 적절한 사이즈의 코드가 적절한 타이밍에 로드될 수 있도록 하는 것!` 
* [리액트 공식문서 코드분할](https://ko.reactjs.org/docs/code-splitting.html)
* 그 중에서도 `Route-based code splitting` 을 사용해본다!

### Suspense, lazy 사용하기
* 코드 자체를 라우팅이 된 시점에 불러오기 때문에 chunk 파일을 분리할 수 있다. → 페이지별로 코드분할하는 방법
```js
import React, { Suspense, lazy } from "react";

const ListPage = lazy(() => import('./pages/ListPage/index'))
const ViewPage = lazy(() => import('./pages/ViewPage/index'))
...
<Suspense fallback={<div>로딩중...</div>}>
...
  <Route path="/" component={ListPage} exact />
  <Route path="/view/:id" component={ViewPage} exact />
...
</Suspense>  
```

<br/>

그렇다면 확인해보쟈 <br/>
<img width="1084" alt="스크린샷 2023-01-08 오후 11 24 15" src="https://user-images.githubusercontent.com/104333249/211201510-40883aec-75ee-4368-8295-64cf1238683f.png">
* chunk 파일이 분리된 것을 볼 수 있다. 그렇다면 네트워크 탭에서 js 파일 다운로드를 확인해보면 <br/>
* 처음 리스트 페이지를 로딩했을 때 불러오는 js 파일이다.
<img width="767" alt="스크린샷 2023-01-08 오후 11 26 25" src="https://user-images.githubusercontent.com/104333249/211201635-871ab14f-1772-41e6-a843-45f84cf1e9ab.png">
* 그 후 디테일 페이지 (viewPage) 로딩했을 때 불러오는 js 파일이다.
<img width="859" alt="스크린샷 2023-01-08 오후 11 26 39" src="https://user-images.githubusercontent.com/104333249/211201641-452de6b1-68e7-4157-84a9-0a80fa4605c0.png">

<br/>

전에 해당 방법을 사용해본적이 있으나 오래 걸리는 컴포넌트 렌더링을 조금 늦추나? 했지만 이럴때 사용하는 것인지 모르고 사용했었다..! 확실하게 눈으로 로딩되는 속도가 줄어드는 것을 보니 신기하당.

<br/>
<br/>









