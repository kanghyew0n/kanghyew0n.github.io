## SWR VS React-query
* React-query는 Devtools가 존재하지만 SWR은 지원되지 않는 기능이다. Devtools를 활용하면 내부 작업을 시각화 할 수 있다는 장점이 있다.
* React-query는 가비지 컬렉션이 가능하다. 캐시된 데이터는 일정 시간이 지나면 수집된다. 이것은 캐시 타임으로 설정도 가능하다. 하지만 SWR에는 별도의 기능이 포함되어 있지 않다.
* 두 라이브러리 모두 mutation을 지원한다. React-query에 비해 SWR은 수동으로 자동해줘야 하기 때문에 불편함이 있다.
