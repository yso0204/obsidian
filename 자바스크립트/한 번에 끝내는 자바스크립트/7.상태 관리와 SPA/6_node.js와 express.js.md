# node.js

node.js는 크롬의 v8엔진으로 빌드된 또 다른 js의 실행 환경, 즉 런타임 환경이다.
하지만 node.js로만 복잡한 웹서버를 구축하는 것은 번거롭고, 시간이 많이 소요 될 수 있어 express 라는 node.js에 구축된 프레임워크를 사용한다.
# express.js
> node.js 의 기능을 확장하여 복잡한 라우팅, 요청처리, 응답처리를 쉽게 관리할 수 있다.

`npm init -y` , `npm install express`

```
const express = require('express');
const path = require('path');
const app = express();
const PORT = 3000;
```
- node.js의 프레임워크인 express 모듈 불러오기
- 파일 시스템의 경로를 다루기 위해 사용되는 path 모듈 불러오기
- express 함수를 호출해서 express 애플리케이션 객체를 생성
- 서버가 계속해서 듣고 있을 포트 번호 설정

![](https://i.imgur.com/hONDgvy.png)

우리가 원하는 건 이러한 구조에서 서버가 항상 `index.html`을 반환해 주는 것

`app.use`라는 메서드를 사용하여 express 애플리케이션에 미들웨어를 추가해준다.

미들웨어란, express.js와 같은 웹 프레임워크에서 `request`와 `response`객체를 수정 및 종료하고, `request`를 보내는 기능을 할 수 있도록 도와주는 함수

`app.use(express.static(__dirname + './..'));` 
이렇게 `express.static()`을 사용하면 정적 파일을 제공하는 미들웨어를 생성할 수 있다. `static`함수에는 제공할 정적파일, 여기서는 `index.html`에 접근할 수 있도록 `server.js`파일의 상위 폴더를 지정

`__dirname`을 사용하면 현재 파일의 경로를 쉽게 작성할 수 있고, `/..`를 사용해 `server.js`파일의 상위 폴더의 경로를 지정

다만, 아래와 같이 window, unix 계열에서 path 구분자가 다르므로, `path`모듈을 사용하여 경로를 설정
```
// console.log(__dirname + '\\..'); // Windows 경로 구분자
// console.log(__dirname + '/..');  // POSIX 경로 구분자 (Unix 계열)
```

# HTTP
> 웹에서 클라이언트와 서버간에 데이터를 주고 받기 위한 규칙
> 