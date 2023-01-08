# Performance Optimization - 성능 최적화
성능 최적화? 필요한 이유는 무엇일까욥 <br/>
페이지가 로딩되는 속도가 느릴수록 사용자의 이탈률이 늘어날 것이다 → 수익이 감소한다, 즉 성능 최적화로 페이지 로딩 속도를 줄여 사용자가 떠나지 않도록 해서 수익을 증대할 수 있게 된다. <br/>

### ? 그렇다면 웹 성능을 결정하는 요소는 ?
* 로딩성능 : 리소스를 불러오는 성능
* 렌더링 성능 : 불러온 리소스를 화면에 보여주는 성능
→ 어떻게 리소스를 불러오고 빠르게 보여줄 것인가!

<br/>


## 💡 Lighthouse 사용해보기
사용해본 적은 있지만 제대로 알고 사용하지 않았던 lighthouse! 전에는 이름이 Audits 였던 것 같다. 기능 추가된 부분이 있는 것 같은데 비슷하다. <br>
나의 목적은 성능 최적화이기 때문에 설정을 Desktop → Performance로 체크하여 사용했다. 

### [METRICS] 검사 지표 <br/> 
<img width="833" alt="스크린샷 2023-01-08 오후 5 06 23" src="https://user-images.githubusercontent.com/104333249/211186429-3f20835c-0cff-456c-a5f2-bd5710303277.png">

### [OPPORTUNITIES] 리소스의 관점에서 가이드 → 로딩 성능 <br/>
<img width="700" alt="스크린샷 2023-01-08 오후 5 14 08" src="https://user-images.githubusercontent.com/104333249/211186674-737ffd1a-d4b0-42b7-b4db-f774c01b35f9.png">

### [DIAGNOSTICS] 페이지 실행 관점 → 렌더링 항목 <br/>
<img width="709" alt="스크린샷 2023-01-08 오후 5 14 52" src="https://user-images.githubusercontent.com/104333249/211186694-b9483888-0d95-4c7c-b681-95e95d7b59cd.png">

### [PASSED AUDITS] 잘 적용한 항목

<br/>


# 이미지 최적화
### 🔺 Properly size images : 적절한 크기의 이미지
* 화면에 표시되는 이미지의 사이즈로 불러오는 것이 적절할까? Retina display에서는 화면에 표시되는 이미지 사이즈 * 2를 사용하는 것이 적절 (고밀도로 더 많은 픽셀을 담고 있어서)
* 이미지를 줄이기 위해서는? 이미지 CDN 사용, 코드에서 받는 이미지 사이즈를 줄여줌 
* 이미지 CDN 사용 → CDN(contents delivery network) : 물리적 거리의 한계를 극복하기 위해 소비자와 가까운 곳에 콘텐츠 서버를 두는 기술 → 이미지를 리사이징까지 하는 것!
([이미지 CDN 주소](https://imgix.com/?utm_term=imgix&utm_campaign=Adwords+-+Branded+-+Asia&utm_source=adwords&utm_medium=ppc&hsa_acc=8534109361&hsa_cam=13353590832&hsa_grp=122727831986&hsa_ad=605794033337&hsa_src=g&hsa_tgt=kwd-316686044535&hsa_kw=imgix&hsa_mt=e&hsa_net=adwords&hsa_ver=3&gclid=CjwKCAiA8OmdBhAgEiwAShr40wGr1YMLHmxTwVNsfyXQwobMHF2FYdUIHX0CbOqGmiuykczM4iaa2xoC6pYQAvD_BwE))
* 코드 내 이미지 사이즈 변경 → unsplash에서 제공하는 이미지 프로세싱 함수
```js
function getParametersForUnsplash({width, height, quality, format}) {
  return `?w=${width}&h=${height}&q=${quality}&fm=${format}&fit=crop`
}
...
<div className={'Article__thumbnail'}>
  <img src={props.image + getParametersForUnsplash({width: 240, height: 240, quality: 80, format: 'jpg'})} alt="thumbnail" />
</div>
```

<br/>


### 결과적으로!
[이미지 최적화 전] <br/>
<img width="700" alt="스크린샷 2023-01-08 오후 5 14 08" src="https://user-images.githubusercontent.com/104333249/211186674-737ffd1a-d4b0-42b7-b4db-f774c01b35f9.png">


[이미지 최적화 후] <br/>
<img width="660" alt="스크린샷 2023-01-08 오후 5 43 07" src="https://user-images.githubusercontent.com/104333249/211187696-0ffe2f30-7fb2-415e-858c-aae76c09d1a3.png">


<br/>
<br/>

