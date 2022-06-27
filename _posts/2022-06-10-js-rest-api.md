---
layout: single
title: "[네트워크] REST API"
categories:
  - 네트워크
tags:
  - api  

---

### REST API란?

API는 다른 sw시스템과 통신하기 위해 따라야 하는 규칙이다.  `REST API`에서 REST (REpresentational State Transfer)는 API **작동 방식에 대한 조건을 부과**하는 소프트웨어 아키텍처이다!

* 웹 (http)의 장점을 최대한 활용할수 있는 아키텍쳐 
* 웹에서 사용되는 **자원(resource)를 HTTP URI로 표현**하고 => 요청 모습 자체로 동작과 정보의 추론이 가능함 !
* HTTP 프로토콜을 통해 **요청과 응답을 정의**하는 방식 

</br>

### REST API 디자인 방법 (REST 성숙도 모델 RMM)

#### 0단계 : HTTP 사용

* HTTP 프로토콜 따르기 

#### 1단계 : 개별 리소스와의 통신 준수 

* 개별 리소스에 맞는 엔드포인트 사용 -> 엔드포인트는 동사가 아닌 명사로 표현한다.
  * 엔드포인트 (Endpoin) : 메소드는 같은 URL들에 대해서도 다른 요청을 하게끔 구별하게 해주는 항목 (ex-1번 00정보)

* 요청하고 요청 받는 자원에 대한 정보를 응답으로 전달 



#### 2단계 : HTTP 메소드 원칙 준수 

* CRUD 에 맞게 적절한 HTTP 메서드 사용
* `GET` : 데이터를 조회(READ) 하는 데에 사용됨 -> `GET` 으로도 나머지를 표현할 수 있지만 `REST`에 적합하지 않다.
* `POST` : 요청시 새로운 리소스 생성(CREATE) `body`에 내용을 실어보냄 
* `PUT` : 새로운 정보(UPDATE)를 `body` 에 실어보냄 -> 교체 (정보를 통째로 갈아끼움)
* `PATH` : 새로운 정보(UPDATE)를 `body` 에 실어보냄 -> 수정 (정보중 일부를 변경)

```
# bad
GET /todos/delete/1

# good
DELETE /todos/1
```

* `{ id: 1, name: 'hywn' }` 유저 리소스의 이름을 수정하려고 할 때 `PUT`과 `PATH`의 차이 

```
PUT /users/1
{ id: 1, name: 'hyewon' }

PATCH /users/1
{ name: 'hyewon' }
```



#### 3단계 : HATEOAS 원칙 준수 

* HATEOAS(Hypertext As The Engine Of Application State)
* 하이퍼 미디어 컨트롤 적용 ->  하이퍼미디어를 애플리케이션의 상태를 관리하기 위한 매커니즘으로 사용한다는 것
* 응답에는 리소스의 URI를 포함한 링크요소를 삽입하여 작성함 -> 새로운 기능에 접근 가능하도록 

```
{
  ...,
  "_links":{
      "self":{
        "href":"http://localhost/api/events/1"
      },
      "query-events":{
        "href":"http://localhost/api/events"
      }
  }
}
```

</br>

</br>
