# 마지막 리뷰 (09.27 ~ 10.10)
### ✅ 새로 알게 된 점 1 : cloudinary
이미지 업로드를 하기 위해서는 두가지 방법이 있다 (내가 아는 것은) <br/>
선택한 방법은 2번! 이미지를 URL로 변환해서 사용하면 백도 프론트도 편할 것 같았다! 
1. 로컬 이미지를 받아 백엔드에서 처리하고 프론트는 이미지 URL만 받아 처리한다.
2. 프론트에서 이미지를 URL로 변환하여 URL만 백엔드에게 보낸다.

* [cloudinary](https://cloudinary.com/) 에 가입해서 
* Dashboard로 이동하여 키, 클라우드 이름 등을 env 파일에 저장한다.
* 무료 계정이 1GB밖에 안되기때문에 이번 프로젝트에서 사이즈 크기를 3MB로 제한을 두었다.
```js
    let formData = new FormData();
    formData.append("api_key", import.meta.env.VITE_CLOUD_API_KEY);
    formData.append("upload_preset", import.meta.env.VITE_CLOUD_PRESET_NAME);
    formData.append("timestamp", (Date.now() / 1000) | 0);
    formData.append(`file`, ref.current.files[0]);

    await instance
      .post(import.meta.env.VITE_CLOUD_API_URL, formData)
      .then((res) => {
        setPlaceImage(res.data.url); // 이미지 주소를 담아주었다!
      })
      .catch((err) => console.log(err))
```

<br/>

### ✅ 새로 알게 된 점 2 : axios instance & JWT access token
* JWT를 사용하여 토큰을 가지고 사용자의 권한을 확인해야 했다.
* axios instance를 사용하여 request / response 전에 interceptors로 토큰을 헤더에 보내기로 했다.
* 아쉽게도 access token 까지만 사용하여 refresh token으로 access token을 재발급받는 과정은 해보지 못했다.

<br/>


### ⚠️ 겪은 문제점 1: axios instance & JWT access token
[ 헤더값 찾기 ]
* 요청헤더에는 토큰값이 오는 것을 확인할 수 있었지만 로컬스토리지에 저장할 수 없었다.
* 헤더에 있는 authorization에 접근이 안되는 것 같아 구글링 해본 결과 `config.addExposedHeader("Authorization")`으로 Authorization 항목을 프론트에서 읽을 수 있게 해준다!

[ 테스트 도중 500 에러가 여러번 발생]
* 첫번째에서는 백엔드의 filter 부분에 오류가 있었다. 
  * 보통 토큰을 보낼때 Bearer과 함께 보내는데 filter로 걸러지는 부분에 조건이 잘못되었었다. 
  * Bearer의 의미 : `Authorization: <type> <credentials>` 에서 인증 타입을 의미하고, Bearer는 JWT 혹은 OAuth에 대한 토큰에 대한 인증타입이다.
* 두번째는 프론트 인터셉터에서 문제가 있었디.
  * 우리는 로컬스토리지에 토큰을 저장했는데 잘못된 (유효하지 않은) 토큰이 저장되었다고 해서 확인해보았다.
  * `.interceptors.response.use` 부분에서 `localStorage.setItem("access_Token", response.headers.authorization.split(' ')[1])`로 저장하고 있었다. (.split(' ')[1]은 Bearer를 제외한 토큰값만을 의미한다)
  *  이때 생각도 못한 Dot Notation, Bracket Notation 개념이,,, ㄴㅇㄱ
  *  Dot Notation : 변수할당 불가능, 띄어쓰기 포함 불가능...
  *  `localStorage.setItem("access_Token", response.headers["authorization"].split(' ')[1])` 로 해결했당!


<br/>

### ⚠️ 겪은 문제점 2: cloudinary & axios instance
[ CORS 오류 ]
* 이미 proxy와 백엔드의 처리(밑에 성명)로 cors 권한을 허용시켰지만 이미지를 업로드 하는 과정에서 에러가 자꾸 발생했다.
* 이미지를 업로드 하는 과정에서 header를 추가해서 보내보기도 하고 `vite.config.js` 파일에서 cloudinary 부분 설정도 다시 해주었지만 원인을 찾지 못했다.
* 결과적으로 axios instance의 영향때문이었다. 
* 우리는 header에 token을 함께 보내는 instance와 보내지 않는 instance를 구분해놨기에 후자를 선택하여 바꿔주었더니 다른 에러가 발생했다.
* 이미지는 `form-data`형식을 사용하기때문에 기존 instance를 사용했을 시 에러가 나는 원인이 됐었다. (기존 instance는 헤더에 json 타입을 받고있기 때문)
* 따라서 우리는 이런 instance를 따로 추가하여 에러를 해결할 수 있었다.
```js
const instance = axios.create({
  header: { "Content-Type": "multipart/form-data" },
})
```
* 백엔드 처리는 `config.addExposedHeader("Authorization")`로 프론트 단에서Authorization 항목을 읽을 수 있게 허용해주었다.


<br/>


### ✅ 새로 알게 된 점 3 : vite html에 env 파일 설정하기
* 기존에 자주 사용했던 CRA (create react app)과 VITE의 사용 방식에는 사소한 차이가 있었다.
* env 설정에서 VITE는 VITE_를 포함한 변수명을 사용해야 하며, `import.meta.env.VITE_`로 사용 가능했다.
```js
// .env
VITE_BASE_URL = "http://125.178.94.154:8080"
```
```js
// 사용 파일
const BASE_URL = `${import.meta.env.VITE_BASE_URL}`;
```

<br/>

### ✅ 새로 알게 된 점 4 : 리액트에서 주소 API 사용하기
* API를 활용한다고 하면 키 발급부터 환경변수 설정, 사용 방법이 익숙하지 않아서 조금 번거로운(?) 작업들이 있는데 주소 API는 활용도 정말 많이 되고 사용이 간단했다! 
* 주소 API를 검색했을 때 다양한 방법이 있지만 나는 다음 [우편번호 서비스(kakao)](https://postcode.map.daum.net/guide)를 사용했다.
* 이유는 사용하기에 가장 친절하고 친숙했기 때문! 반환되는 데이터를 어떻게 찾아야하는지, 활용 방법까지 나와있었다. (카카오 지도 API와 함께 쓰기에 확장성을 고려했을때 좋다고 판단했다.)
* 우리가 필요한 서비스는 정확한 주소 입력이었기 때문에 사용자가 검색하면 string값으로 주소를 받고싶었다.
* 리액트에서 사용했기 때문에 패키지를 설치해주었다.
```js
npm install react-daum-postcode
```
```js
import DaumPostcodeEmbed from 'react-daum-postcode';
...
<DaumPostcodeEmbed/>
// 사용해주면 된다.
```
* `fullAddress` 값을 받아 state로 주소를 관리해주었다.
* pop up 형태로 뜨길 원했어서 모달로 <DaumPostcodeEmbed/> 를 감싸주었다.
* 주소를 입력했을때는 자동으로 닫아지지만 사용자가 실수로 눌렀을때, 혹은 주소를 입력했는데 창을 닫고싶을때 방법이 없기 때문에 닫기 버튼을 만들어주는 추가 작업을 진행했다.


<br/>

### ✅ 새로 알게 된 점 5 : vercel 배포
* 아쉽게도 백엔드 단에서는 배포를 하지 못했지만 프론트라도 하기위해 vercel로 배포를 진행했다.
* 우선 env설정을 모두 해주고 배포를 1차로 진행했다.
* 얼마 못가 에러가 났는데 원인은 이미지 형식에 대한 에러였다.
* 사잍으에서 사용하는 이미지 대부분 svg 형식이지만 png 형식도 존재하는데 vercel 에서 `.png` 파일이 `.PNG` 파일로 저장되어있을 경우 인식을 하지 못했다. (로컬에서는 문제가 없었지만..) 모두 바꿔주도 다시 배포를 시도했다.
* 다시 실패했는데 이유는 패키지 버전 문제였다. 
* 같은 프론트엔드 분이 설치하신 라이브러리에서 install이 안되는 현상이 보여서 `npm install --force`를 추가하여 빌드해주었더니 성공했다!
* `npm install --force` : -for --force인수는 로컬 복사본이 디스크에 있더라도 npm이 원격 리소스를 가져오도록 합니다. [npm docs](https://docs.npmjs.com/cli/v6/commands/npm-install) 참고




<br/>

### 👍 잘한 점
* 프리 프로젝트때도 많은 성장을 했다고 생각했는데 메인 프로젝트는 기술 사용에 있어 자유로워진 느낌이다! 
* vite, zustand, swr 등 처음 사용해보는 기술들을 익히며 자신감도 얻고 거부감이 상당하게 줄었다. 뭐든 습득할 수 있구나 하고 느꼈다 🧐
* 기술뿐만 아니라 협업에 있어서도 많은 것을 느꼈다, 가장 중요한 것은 소통이다! 같은 프론트끼리도 백엔드와도 가장 중요한 것은 소통이고 소통은 과할수록 좋다는 것을 다시 느꼈고
* 원하는 부분이 있다면 명확하게 근거와 함께 전달해야 나에게도 상대방에게도 효율적이라는 것을 알게 되었다. 💭💬
* 팀원들 덕분에 끝까지 타협하지 않고 할 수 있었다. 혼자 했다면 여기까지만, 이정도로 만족.... 을 했을텐데 팀원들과 함께 하니 끝까지 한 느낌이다.
* 필터, 검색, 카테고리 부분을 맡고 내가 생각한 데이터 형식과 다른 형식이 와서 코드를 대폭 수정한 일이 있었는데 (이것 또한 소통의 부재라고 생각한닷) 그래도 막힌 부분에서 언어가 다르지만 백엔드 팀원의 도움을 받기도 하고 다른 팀원을 보며 결국엔 성공해냈다..! 정말 감격 🥹

<br/>


### 🥲 아쉬운 점
* 원하는 기능 모두를 달성하지 못한 점 (소셜 로그인이나 지도부분)
* 기간에 쫓기듯 작업한 점 : 이럴 경우 코드가 복잡해지고 팀 간의 소통이 줄어든다고 생각한다. 🥲
* 팀에서 이슈가 있던 점.. 원활하게 흘러갔을 수도 있지만 빠르게 대처를 잘 하지 못했나 반성,,


<br/>


### 🚀 추가적으로
* 프로젝트가 끝났으니 부족한 부분을 채워야겠다! 병목되지 않으리,,
* 역시 재밌간 하다 재밌다! 물론 힘들지만 하나하나 만들어가면 성취감이 😇 구뜨 재미가 


<br/>
<br/>

