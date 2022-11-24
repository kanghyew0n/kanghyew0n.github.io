# 브라우저 렌더링 원리

렌더링 엔진이 HTML, CSS, Javascript 로 렌더링할 때 CRP라는 프로세스를 사용한다. CRP 는

- HTML 파싱 후 [DOM](https://github.com/kanghyew0n/My-Book/blob/main/JavaScript/2022-05-17-%5BJavaScript%5D%20%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%20DOM.md) 트리를 구축하고
- CSS 파싱 후 CSSOM트리를 구축한다.
- 그 후 JavaScript를 실행한다.
- DOM과 CSSOM을 조합하여 렌더트리를 구축한다.
- Layout 단계에서는 뷰포트 기반으로 렌더트리의 각 노드가 가지는 정확한 위치와 크기를 계산한다.
- Paint 단계에서는 계산한 위치/크기를 기반으로 화면에 그린다.

<br/>

### ⚠️ 주의

- HTML 중간에 스크립트가 있다면 HTML 파싱이 중단됨
- `display: none` 속성과 같이 화면에서 보이지도 않고 공간을 차지하지 않는 것은 렌더트리로 구축되지 않음

<br/>

### 💬 용어
**CRP (Critical Rendering Path, 중요 렌더링 경로)** 는 <br/>
브라우저가 HTML, CSS, Javascipt를 화면에 픽셀로 변화하는 일련의 단계!

<br/>

**파싱은** <br/>

브라우저가 코드를 이해하고 사용할 수 있는 구조로 변환하는 것을 의미한다. 즉,  파스 트리(parse tree)를 생성하는 과정
파싱은 보통 문서를 다른 양식으로 변환하는데 컴파일이 하나의 예가 된다. 소스 코드를 기계 코드로 만드는 컴파일러는 파싱 트리 생성 후 이를 기계 코드 문서로 변환한다.

<br/>

**DOM(Document Object Model)이란** <br/>
웹 페이지를 이루는 태그들을 자바스크립트가 이용할 수 있게끔 브라우저가 트리구조로 만든 객체 모델을 의미한다.

<br/>

**CSSOM(CSS Object Model)이란** <br/>
CSS 내용을 파싱하여 자료를 구조화 한 것을 CSSOM이라고 한다. 즉 DOM처럼 CSS의 내용을 해석하고 노드를 만들어 트리 구조로 만든 것을 CSSOM이라 한다.
<br/>

**렌더 트리는**  <br/>
CSSOM과 DOM 트리의 결합으로 만들어진다. 렌더 트리는 웹 페이지에 나타낼 각 요소들의 위치(Layout, 레이아웃)을 계산하는데 사용되고 픽셀을 화면에 렌더링하는 페인트(Paint) 
즉 화면에 요소들을 표현하는 프로세스를 위해 존재한다.

<br/>
<br/>
