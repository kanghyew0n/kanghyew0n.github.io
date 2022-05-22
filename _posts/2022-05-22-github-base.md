---
layout: single
title: "[Github] 처음 시작하기"
categories:
  - Github
tags:
  - Github  
  - 프로젝트 생성   

---



**시작하면서** 

프로젝트를 진행하면 버전관리가 필요하게 된다. 프로젝트가 진행될수록 최종 파일, 최근 파일이 무엇인지 분간이 어렵기 때문이다. 프로젝트를 한 번 해보면 알게된다... 최종.zip, 진짜최종.zip, 이게진짜최종!!!.zip,,,,,

실제로 졸업작품으로 프로젝트를 진행했을 당시 실화다,, 그래서! 깃허브를 사용하여 효율적으로 버전관리를 할 수 있어야한다!!!

`git` 

* 소스코드를 효과적으로 관리하기 위해 개발된 '분산형 버전관리 시스템'
* 로컬에서 버전 관리 
* 하나의 프로젝트, 같은 파일을 여러사람과 동시에 사용이 가능함

`github`

* 분산 버전 관리 툴인 `깃(Git)`을 사용하는 프로젝트를 지원하는 웹호스팅 서비스 
* `git` 으로 관리하는 프로젝트(코드)들을 `github` 에서 관리(업로드)할 수 있다.

 둘의 차이를 몰랐을때는 `git === github` 이었다. 하지만 아니라는 점! 

어떤 글을 봤는데 `git` 은 동영상 어플이고 `github`은 유튜브라는,, 이해가 조금 됐다! 그럼 이제 `github`을 활용하여 프로젝트와 블로그를 올려보자!!

  

<u>운영체제 ubuntu 18.04</u>



### [Github] 처음 시작하기

* 우분투 터미널에서 복사 & 붙여넣기를 하고싶다면 `Ctrl + Shift + C` & `Ctrl + Shift + V`
* 시작하기 전에 `github `가입하기!

#### 1. Git 설치하기 

[설치링크](https://git-scm.com/download/linux) 혹은 터미널로 설치할 수 있다!

터미널을 열고 (Ctrl + Alt + T)  `sudo apt install git` 을 입력해 패키지 git을 설치한다.

```
1.  sudo apt install git //git 설치 
2.  git --version //git 버전 확인 -> 잘 나오면 설치 완료!
```



#### 2. 초기설정 

사용자의 이름과 이메일을 등록해주고 에디터도 설정해준다.

merge commit 확인 메시지가 나올 때 텍스트 에디터가 열리는데 기본값은 vi지만 익숙하지 않다면 nano로 변경하기 

```
git config --global user.name "사용자 이름" 
git config --global user.email "사용자 이메일"
git config --global core.editor nano 

git config --list // 등록한 후 확인 가능 
```



#### 3. SSH 이용하기 

ssh 등록하면 username과 password를 입력하지 않고 git과 인터렉션 할 수 있다 라고 하는데 ( [참고한 블로그](https://devocean.sk.com/blog/techBoardDetail.do?ID=163311) ) 저도 등록을 했습니다만 매번 username과 password를 입력합니다..

아 그리고 ssh 키를 등록하지 않으면 `git permission denied (publickey)` 라는 허가거부 에러를 받을 수 있다는 점 


<u>**! 번외 **</u>) 

> **upport for password authentication was removed on august 13, 2021.** 
>        **please use a personal access token instead**

이 에러가 나올 수 있는데 이는

> ***2021년 8월 13일 부로 "비밀번호로 인증"하는 방식이 더이상 사용할 수 없게 됨에 따라***, ***개인 토큰 (a personal access token) 을 새로 발급받아서 인증해야 GitHub API 에 접속할 수 있다*** 

는 뜻이다 

그렇다면 토큰을 등록하는 방법은 [참고한 블로그](https://hoohaha.tistory.com/37) 입니다닷,, 혹은 git token 이라고 검색하면 많이 나온다!

이때 받아놓은 토큰은 메모장에 따로 저장하고 password를 물어보면 사용하면 된다! 예를들어 `push` 할 때 password 입력에 사용 



#### 4. Github 새로운 저장소를 생성 (프로젝트 생성)

상단 `repositories` 를 선택하고 초록색 `New` 버튼을 클릭하면 아래와 같은 화면이 나온다. (만약 블로그를 만들 것이라면 다음편에서,, )

![image-20220522185035715](../images/2022-05-22-github-base/image-20220522185035715.png)



#### 5.  Git 저장소 만들기 

프로젝트를 생성한 파일로 이동을 먼저 해주어야한다. 이동한 후에 `init` 해준다. 이는 저장소를 초기화 해주는 것이다. 그럼 위에서 생성한 repository에 연동해준다. 

```
cd 원하는_폴더_명
git init
git remote add origin https://github.com/~ 
```

`remote add origin 주소`  에서 주소는 밑에 사진에서 `code` 를 클릭하고 나오는 창에서 복사해온다!

![image-20220522185911402](../images/2022-05-22-github-base/image-20220522185911402.png)

#### 6. 로컬에 있는 파일 repository 에 push

```
git status // 상태확인 -> 빨간 글씨로 업로드 안된 파일명이 뜬다.

git add . //파일 모두 업로드 
git add 해당파일명.txt //원하는 파일 하나만 업로드 

git status // 상태확인 -> 초록 글씨로 업로드 될 파일명이 뜬다.

git commit -m "커밋 메세지" //커밋해준다 -> -m 은 메세지를 적는 것 

git remote -v //origin 의 url확인 

git push origin main (혹은 master) //push 해준다! 이때 username 과 password를 물어본다면, 이름 입력하고 password는 위에서 말한 token을 입력해준다.
```

 

#### 7. Pull request

위의 과정이 완료됐다면 자신의 repository로 가보자 , 그럼 아래 사진처럼 나와있을텐데 저 초록색 버튼을 클릭하자!

![image-20220522192032141](../images/2022-05-22-github-base/image-20220522192032141.png)

그 다음 계속해서 초록색 버튼을 눌러주면 보라색으로 바뀐다. 그럼 성공! 다시 <> 코드 메뉴로 돌아가보면 아래 사진처럼 되어있을텐데 저 노란색 동그라미가 초록색 체크로 변하면 완료!

![image-20220522192318232](../images/2022-05-22-github-base/image-20220522192318232.png)
