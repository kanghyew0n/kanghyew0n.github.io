---
layout: single
title: "[React] React State & Props (Advanced Challenge)"
categories:
  - react
tags:
  - 리액트   
  - state  

---

### React State & Props (Advanced Challenge)

 BareMinimum 테스트는 페어분과 어떻게 해서 이해를 했지만 advanced는 생각조차 하지 못했다! 그러다가 페어분께 조금 힌트를 얻고 세션때 들은 수업을 바탕으로 아이패드에 끄적이며 이해하려고 노력했다. 코드를 보고 치고싶지는 않아서 이해한 내용을 정리해서 그걸 바탕으로 코드를 작성했다. (물론 다른 분들이 보면 다 적은거 아니냐고 할 수 있지만 ,, ㅜ)

정리한 내용은 요러하다! (잘못된 부분이나 오타가 있을 수 있습니다,, )

<br/>

![select](/home/kanghyew0n/카카오톡 받은 파일/select.jpg)

<br/>

### Select, Option

#### 코드 작성 순서는 이렇다!

1. state로 관리되어야 할 항목을 지정한다.

​		a. select 에서 option으로 선택됐는지 여부 

​		b. Tweet 컴포넌트에 선택된 username의 tweet만 가져오기 

2. `<select> ` 를 생성하여 tweets에 있는 username을 `<option>` 을 통해 보여주어야 한다. 

​		a. 전체를 보여주는 옵션(1) 과 

​		b. tweets에 있는 username을 보여주는 옵션(2) 이 필요하다.

3. select 된 username인지 함수를 통해 판별한다.

​		a. 함수를 생성하고 옵션에서 선택된 것이 무엇인지 (1) 인지 (2) 인지 

​		b. tweet에 어떤 데이터를 담을 것인지 

4. 화면에 직접 보여질 ( `<ul>`에 담길 ) tweet을 가져오기 

   a. 함수를 통해 걸러진 (선택된 username) tweet 가져올지 

   b. tweets에 있는 전체 tweet 가져올 것인지 

<br/>

#### 1. state로 관리되어야 할 항목을 지정하기 

* select 에서 option으로 선택됐는지 여부 : 필터로 걸러졌는가? (초기값 false)

```js
  const [isFiltered, setIsFiltered] = useState(false);
```

* Tweet 컴포넌트에 선택된 username의 tweet만 가져오기 : 필터로 걸러진 tweet인가? (초기값 dummyTweets 전체 데이터 )

```js
const [filteredTweets, setFilteredTweets] = useState(dummyTweets);
```



#### 2. `<select> ` 를 생성하여 tweets에 있는 username을 `<option>` 을 통해 보여주기 

* 전체를 보여주는 옵션 (1) 

```js
<select>
 	<option value="all"> -- click to filter tweets by username --</option>
</select>
```

* tweets에 있는 username을 보여주는 옵션(2) 

```js
  // options에 username만 담은 데이터를 보관
  const options = tweets.map((data) => {
    return <option value={data.username}>{data.username}</option>;
  });
```

* 전체  `<select>` 부분

```js
<select>
 	<option value="all"> -- click to filter tweets by username --</option>
	{options}
</select>
```



#### 3. select 된 username인지 함수를 통해 판별 (함수생성)

* 함수를 생성하고 옵션에서 선택된 것이 무엇인지 (1) 인지 (2) 인지 / tweet에 어떤 데이터를 담을 것인지 
  * 옵션 (1) : `event.target.value === "all"` -> 전체 /  setTweets(tweets) -> 젠체 데이터 
  * 옵션 (2) : `else` -> {options} / setFilteredTweets(filtered) -> 필터된 tweet

```js
  const handleFilter = (event) => {
    if (event.target.value === "all") {
      setIsFiltered(false);
      setTweets(tweets);
    } else {
      const filtered = tweets.filter((tweet) => {
        return tweet.username === event.target.value;
      });
      setIsFiltered(true);
      setFilteredTweets(filtered);
    }
  };
```



#### 4. 화면에 직접 보여질 ( `<ul>`에 담길 ) tweet을 가져오기 

* 삼항연산자로 isFiltered ? : 
  * 함수를 통해 걸러진 (선택된 username) tweet 가져올지 
  * tweets에 있는 전체 tweet 가져올 것인지 

```js
	{isFiltered ? filteredTweets.map((tweet, idx) => {
        return (
            <Tweet tweet={tweet} key={tweet.id}/>
          );
      })
     : tweets.map((tweet, idx) => {
        return (
             <Tweet tweet={tweet} key={tweet.id}/>
         );
     })}
```

<br/>

> 초반에 많이 헤맸던 이유는 state로 관리 해 주어야 할 항목을 잘 몰라서 인 것 같고, 코드를 작성하면서 가장 많이 발생한 오류는 props에 key가 없다는? 거였는데 그 부분도 신경쓰기 어려웠다! (검색하면 바로 나오기도 함!) 

<br/>

### Delete

#### 코드 작성 순서는 이렇다!

1. 삭제 버튼을 생성하고 `onClick`시 함수 호출하게 하기 (함수 : `handleDelete`)
2. 함수 ) 선택된 버튼의 idx를 제외한 나머지를 `Tweet` 컴포넌트에 담아주기

​		a. 매개변수를 username, deleteIdx로 주고 

​		b.  deletes 라는 변수를 생성하고 필터로 `idx !== deleteIdx` 인 것만 담아주기 

3. 삭제버튼이 눌린 idx 를 제외하고 tweet 보여주기 

   a. `handleDelete` 함수를 Tweet 에서 실행하고 idx도 부여해주기 



#### 1. 삭제 버튼을 생성하고 `onClick`시 함수 호출하게 하기 (함수 : `handleDelete`)

이건 tweet.js에서 작성해줘야하는 부분임 

```js
<button onClick={() => handleDelete(tweet.username, idx)}>
   	button
</button>
```



#### 2. 선택된 버튼의 idx를 제외한 나머지를 `Tweet` 컴포넌트에 담아주기 (함수 생성)

* 매개변수를 username, deleteIdx로 주고 
* deletes 라는 변수를 생성하고 필터로 `idx !== deleteIdx` 인 것만 담아주기 

```js
 // delete 함수
  const handleDelete = (username, deleteIdx) => {
    const deletes = tweets.filter((tweet, idx) => idx !== deleteIdx);
    setTweets(deletes);
  };
```



#### 3. 삭제버튼이 눌린 idx 를 제외하고 tweet 보여주기 

* `handleDelete` 함수를 Tweet 에서 실행하고 idx도 부여해주기 (위에서 작성한 부분에서 추가해주기)

```js
	{isFiltered ? filteredTweets.map((tweet, idx) => {
        return (
            <Tweet tweet={tweet} key={tweet.id} handleDelete={handleDelete} idx={idx}/>
          );
      })
     : tweets.map((tweet, idx) => {
        return (
             <Tweet tweet={tweet} key={tweet.id} handleDelete={handleDelete} idx={idx}/>
         );
     })}
```

<br/>

완료!

<br/>

> 삭제 부분은 생각보다 간단했지만, onclick된 버튼의 idx를 가져와서 그걸 필터로 제외시켜서 내용을 보여주는 방법이라고는 생각도 못했다! 들으면 이해가지만 혼자 하려면 생각이 안나는 그런,, 것,, 그리고 이것도 마찬가지로 idx를 주고 매개변수를 뭘 주고 이런게 굉장히 어렵고 까다로웠다,, 
>
> 그래도 최종적으로는 손으로 로직을 이해해서 글로 써보고  그걸 바탕으로 코드를 짤 수 있었다! 잘 안풀려서 굉장히 무기력했었는데 그래도 이해하고 코드를 써보니 기분이 다시 좋아졌다! 앞으로도 화이탱!!! 



