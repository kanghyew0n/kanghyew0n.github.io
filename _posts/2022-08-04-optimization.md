---
layout: single
title: "[Optimization] 최적화 기법"
categories:
  - 최적화 
tags:
  - Tree Shaking   
  - Lighthouse  

---




<br/>


## 💡 google 번역 

![Untitled](https://user-images.githubusercontent.com/104333249/182866587-46c5ebd8-9ff6-438f-ad89-5b613cba4d60.png)

### 😌 Performance의 Opportunities 항목

- **사용되지 않는 JavaScript 줄이기**
  - 네트워크 작업에 사용되는 바이트를 줄이는 데 필요할 때까지 스크립트 로드를 연기해라 > 'React.lazy()'로 자바스크립트 번들을 분할해라



<br/>

<br/>



## 💡 파파고 

![Untitled (1)](https://user-images.githubusercontent.com/104333249/182866725-0d21b3fc-b8cd-43b4-8d01-486bda5acd73.png)

### 🤔 Performance의 Opportunities 항목

*(가장 많은 시간이 소요된 항목 순서)*

- **사용되지 않는 JavaScript 줄이기**
  - 네트워크 작업에 사용되는 바이트를 줄이는 데 필요할 때까지 스크립트 로드를 연기해라 > 'React.lazy()'로 자바스크립트 번들을 분할해라
- **JavaScript 최소화**
  - JavaScript 파일을 최소화하면 페이로드 크기 및 스크립트 구문 분석 시간을 줄일 수 있다.
- **렌더 차단 리소스 제거**
- **사용하지 않는 CSS 줄이기**
- **필요한 오리진에 사전 연결**
  - 초기 연결을 설정하기 위해 'preconnect' 또는 'dns-prefetch' 리소스 힌트를 추가하는 것을 고려해라
- **화면 외 이미지 연기**
  - 모든 중요 리소스 로드가 완료된 후 화면 및 숨겨진 이미지를 느리게 로드하여 대화식 작업 시간을 단축할 수 있다.
- **next-gen 형식으로 이미지 제공 ?**
  - WebP 및 AVIF와 같은 이미지 형식은 종종 PNG 또는 JPEG보다 더 나은 압축을 제공하므로 다운로드 속도가 빨라지고 데이터 소비량이 줄어든다.
- **기존 JavaScript를 최신 브라우저에 제공하지 않음**
  - 모듈/노모듈 기능 감지를 사용하여 기존 브라우저에 대한 지원을 유지하면서 최신 브라우저로 전송되는 코드의 양을 줄이도록 하는 최신 스크립트 배포 전략을 채택해라







<br/>

<br/>
