# Performance 탭 확인하기
개발자 도구 Performance를 확인해보쟈. HTML이 파싱되고 JS가 실행되고 코드가 실행되는데 Article 부분에서 실행 시간이 많이 소요되는 것을 볼 수 있다. 특히 removeSpecialCharacter 부분이 반복되며 실행되는데 코드를 살펴보쟈.


<br/>

<img width="1032" alt="스크린샷 2023-01-08 오후 9 08 09" src="https://user-images.githubusercontent.com/104333249/211195227-c2b9e779-ec7f-40db-b30e-50d7ccfc99ee.png">

<br/>

# 🍾 Bottleneck 코드 최적화 
```js
function removeSpecialCharacter(str) {
  const removeCharacters = ['#', '_', '*', '~', '&', ';', '!', '[', ']', '`', '>', '\n', '=', '-']
...
  for (i = 0; i < removeCharacters.length; i++) {
    j = 0
    while (j < _str.length) {
      if (_str[j] === removeCharacters[i]) {
        _str = _str.substring(0, j).concat(_str.substring(j + 1))
        continue
...
```
* 해당 코드는 Article List 부분에서 thumbnail에 해당하는 글로 200-300자 정도 노출되는 글이다.
* removeCharacters 배열에 해당하는 특수 문자가 포함되면 제거하는 코드이다.
* removeSpecialCharacter의 인자로 받는 문자열은 markdown 형식이기 때문에 굉장히 길이가 길다 → 이것 만큼의 길이를 for문으로 돌려서 특정 문자열은 비효율 적이며 여기서 병목 현상이 발생할 수 있다.

<br/>

## Bottleneck 해결방안
* 특수문자를 효율적으로 제거하기
  * replace 함수와 정규식 사용하기
  * 마크다운의 특수문자를 지워주는 라이브러리 사용하기 (remove-markdown)   
* 작업하는 양 줄이기 
  * 200-300자 정도 노출되는 글이지만 전체 글의 문자열을 받아 처리했기 때문에 병목 현상이 일어나는 원인이 될 수 있음 
  * 작업하는 양 자체를 줄여주기

<br/>

## 최적화 후
* 그래프의 폭이 줄었고 시간도 142ms → 0.13ms 확실하게 줄어든 것을 확인할 수 있다!!! <br/>
<img width="1078" alt="스크린샷 2023-01-08 오후 9 33 51" src="https://user-images.githubusercontent.com/104333249/211196254-7ae02999-2331-454b-a7c8-ac915159604c.png">

<br/>
<br/>
