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