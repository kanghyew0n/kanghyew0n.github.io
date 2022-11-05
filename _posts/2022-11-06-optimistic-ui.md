---
layout: single
title: "[Optimistic UI] 낙관적 업데이트"
categories:
  - UI 
tags:
  - react 
  - ui
---

<br/>

## 낙관적 업데이트 N차 실패
> 낙관적 업데이트란 서버에 응답을 받기 전 사용자의 행동에 대란 결과를 미리 반영하는 것을 의미한다.(사용자의 행동이 성공했을 때의 결과) 이것은 좋은 사용자 경험을 준다고 한다 <br/>
> → 우리가 흔히 사용하는 인스타에 좋아요를 눌렀을때 즉각 반응하는 빨간색 하트도 이에 해당할 것이다! 
 
 <br/>
 
그럼 다시, 우리가 리액트를 사용하는 이유에 대해 생각해보자!<br/>
리액트는 깜빡임 없이 사용자의 행동에 반응한다. 즉 사용자에게 한 페이지만을 보여주고 인터렉션이 일어난 부분만 파일만 변경해준다. <br/>

<br/>

하지만 프로젝트에서 그 부분을 잊고있었다. 데이터 통신이 이루어진 후 새로고침 `window.reload()` 를 하지 않으면 데이터가 업데이트 되지 않아 무분별하게 새로고침 코드를 삽입하였다. 🥲 
꽤 최근에 진행한 프로젝트에서는 낙관적 업데이트 + 에러핸들링 + 로딩처리를 잘 하기위해 SWR 을 사용하기도 했지만 에러핸들링 + 로딩처리에만 성공하였다. 그래서 다시 공부해봤다,, swr

<br/>

## 어쩌다 낙관적 업데이트 성공 (?)

낙관적 업데이트에 성공하기위해 swr을 사용하여 시도해보다가 힌트를 얻었다. swr에서 예시를 하나 발견하게 되는데 ([참고링크](https://codesandbox.io/s/swr-basic-forked-k5hps?from-embed))
갑자기 생각났다! 그냥 상태를 하나 추가해서 통신 데이터를 받고 뿌려주는 데이터를 변화된 데이터로 바꿔주면 낙관적 업데이트가 아닌가,, 하는 (아래 예시)
→ 통신은 진행하고 성공한 데이터를 바로 넘겨주는 방법이다!

![Nov-06-2022 02-01-26](https://user-images.githubusercontent.com/104333249/200132176-9821834d-e600-4bb9-8e98-d72811b8acc5.gif)
> 낙관적 업데이트 전 화면 : 새로고침이 필요하다 (아니면 시간이 시간이 좀 걸리거나 화면을 다시 포커스 하면 업데이트 된다 → SWR 기능)  <br/>
> 🙋‍♀️ **사용자 인터렉션 → 사용자 대기 → 서버에 데이터 요청 → 서버 및 클라이언트 반영**


<br/>

![Nov-06-2022 02-00-34](https://user-images.githubusercontent.com/104333249/200132169-4eeb1a7d-68b6-42ff-9a4d-bf032ae847a2.gif)
> 성공했을때 화면 : 깜빡임 없이 업데이트 된 내용으로 바뀐다! <br/>
> 🙋‍♀️ **사용자 인터렉션 → 성공시 반응 (낙관적 업데이트) → 서버에 데이터 요청 → 서버 반영**

<br/>

```js
  const [title, setTitle] = useState(props.item.title);
  const [body, setBody] = useState(props.item.body);
  const [data, setData] = useState(props.item);


  const onUpdate = () => {
    useUpdatePost(data.id, title, body); // hooks로 뺀 api통신 부분
    setData({
      title,
      body
    })
  };
```

<br/>

성공했지만 문제가 있다...  <br/>
데이터 통신 전 사용자 인터렉션에 반응하기 떄문에 에러에 대한 처리를 못한다는 점이다..(좌절) <br/>
그래서 내린 결론 : SWR이나 react query를 괜히 사용하는 것이 아니구나,,,

<br/>

## SWR에서의 낙관적 업데이트 
SWR 공식문서를 확인하면 `mutation`이라는 항목에 낙관적인 업데이트라는 항목이 있다. 이걸 보고 테스트 해보았다. <br/>
우선 낙관적 업데이트를 위해서는 mutate를 사용해야하고 여기엔 옵션이 여러가지 존재한다.
```js
mutate(key, data, options)

const options = {
        optimisticData: something... , //클라이언트 캐시를 즉시 업데이트하기 위한 데이터
        rollbackOnError: true, //비동기 업데이트가 해소되면 캐시를 갱신
        populateCache: true, // 원격 돌연변이의 결과가 캐시에 기록되어야 하거나 새로운 결과와 현재 결과를 인수로 받아 돌연변이 결과를 반환하는 함수
        revalidate: false, //원격 뮤테이션 에러 시 캐시를 롤백
}
```
여기서 optimisticData 옵션을 가지고 데이터를 갱신한다. <br/>
이를 바탕으로 내 코드에 적용해보기로 한다, 우선 고려해야 할 사항이 있었다. 
1. hooks로 분리되어있는 useSWR에서 mutate return 해서 사용하기
2. mutate 가져와서 get 한 data → optimisticData 로 바꿔서 낙관적 업데이트 가능하게 하기 
이렇게 적어보니 간단해보이지만 2번에서 실패하고 말았다.

```js
const { data, isLoading, isError, mutate } = useGetPosts();

const onDelete = async () => {
    if (window.confirm("삭제하시겠습니까?")) {
       await mutate(useDeletePost(props.item.id), {
         optimisticData: data.filter((item) => props.item.id !== item.id), //클라이언트 캐시를 즉시 업데이트하기 위한 데이터
         rollbackOnError: true,
         populateCache: true, 
         revalidate: false, 
       });
    }
  };

```
optimisticData 에서 삭제를 진행하면 해당 아이디 빼고 전체 리스트 데이터를 반환하려 했는데 부모 컴포넌트 (리스트 컴포넌트)에서 에러가 났지만 원인은 찾지 못했다.
훌쩍 





<br/>


<br/>
