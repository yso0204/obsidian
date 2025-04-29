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
이렇게 `express.static()`을 사용하면 정적 파일을 제공하는 미들웨어를 생성할 수 있다. `static`함수에는 제공할 정적파일, 여기서는 `index.html`에 접근할 수 있도록 `server.js`파일의 상위 폴더를 지정(`./..`)

`__dirname`을 사용하면 현재 파일의 경로를 쉽게 작성할 수 있고, `/..`를 사용해 `server.js`파일의 상위 폴더의 경로를 지정

다만, 아래와 같이 window, unix 계열에서 path 구분자가 다르므로, `path`모듈을 사용하여 경로를 설정
`app.use(express.static(path.join(__dirname, '..')));`

```
// console.log(__dirname + '\\..'); // Windows 경로 구분자
// console.log(__dirname + '/..');  // POSIX 경로 구분자 (Unix 계열)
```

# HTTP
> 웹에서 클라이언트와 서버간에 데이터를 주고 받기 위한 규칙

## HTTP 메서드

1. GET : 서버로부터 데이터 요청
2. POST : 서버로부터 데이터 전송
3. PUT : 서버에 데이터 업로드
4. DELETE : 서버에서 데이터 삭제

express에서 get을 하는 방법은 아래와 같다.
```js
app.get('/*name', (req, res) => {
    res.sendFile(path.join(__dirname,'..','index.html'))
})
```
클라이언트에서 요청이 들어오면 `res`을 사용하여 응답으로 `index.html`을 전달


## 라우팅
`express` 애플리케이션에서 서버를 시작하고, 지정한 3000 포트에서 요청을 들을 수 있도록 설정

```js
app.listen(PORT, () => {
    console.log('START SERVER');
});
```

## `server.js`
```js
const express = require('express');
const path = require('path');
const app = express();
const PORT = 3000

app.use(express.static(path.join(__dirname, '..')));

app.get('/*name', (req, res) => {
    res.sendFile(path.join(__dirname,'..','index.html'))
})

app.listen(PORT, () => {
    console.log('START SERVER');
});
```

node로 해당 서버 실행 후 `localhost:3000`에서 확인하면 `/panda`등에 진입 후 새로고침해도 알맞은 화면을 보여주는 것을 볼 수 있다.

| 단계  | 설명                                              |
| --- | ----------------------------------------------- |
| 1   | 브라우저가 `/panda`로 새로고침 요청                         |
| 2   | 서버가 `index.html` 파일을 반환                         |
| 3   | `index.html` 안에서 `src/index.js` 로딩됨             |
| 4   | `App` 객체가 생성될 때 `window.location.pathname`을 읽음​ |
| 5   | `/panda`에 맞게 API 요청해서 판다 사진을 불러옴​               |
| 6   | 화면에 판다 사진이 다시 출력                                |
[클라이언트(브라우저)]
    ↓ (HTTP 요청)
[index.html 요청]
    ↓
[서버: HTML 파일 제공]
    ↓
[index.html에서 src/*.js 파일 추가 요청]
    ↓
[서버: JS 파일 제공]
    ↓
[브라우저: JS 파일 실행, 화면 렌더링]
    ↓
[App.js가 API 서버로 데이터 fetch 요청]
    ↓
[API 서버: JSON 데이터 응답]
    ↓
[Content.js가 사진을 화면에 그려줌]

![](https://i.imgur.com/BFL3OLg.png)
