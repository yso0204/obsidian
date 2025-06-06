# SPA
> 웹이나 웬 애플리케이션의 현대적인 구현 방식 중 하나로, 사용자에게 빠르고 부드러운 사용자 경험을 제공한다. 
> 핵심은 상호작용 중 새로 불러오는 것이 아닌, **필요한 데이터만** 서버로부터 동적으로 불러와 페이지를 업데이트


# 라우팅
> 웹 사이트 내에서 웹 주소(URL)을 특정 페이지에 연결하는 과정
> 이를 통해 사용자가 브라우저에 URL을 입력하거나, 특정 링크 클릭시에 애플리케이션이 요청에 맞는 페이지를 반환할 수 있다.

SPA에서 라우팅은 사용자가 다양한 페이지, 뷰로 이동할 수 있게 하면서도 실제로 전체 리렌더링이 아닌, 필요한 부분만 변경하는 기술로 

페이지 전환 시에 서버에서 HTML을 새로 로드하는 것이 아니라, js를 사용하여 클라이언트 측에서 동적으로 필요한 데이터를 불러오고 콘텐츠를 렌더링한다.

SPA에서는 웹 페이지를 조금 더 직관 적으로 사용할 수 있고, 뒤로 가기, 앞으로 가기 같은 네이게이션 기능을 지원해 사용자가 여러 페이지를 탐색하는 것 처럼 보이게 하기 위해 클라이언트 측에서 라우팅을 처리하는 것이 일반적

React Angular, Vue 등에서는 프레임워크 측에서 자체적인 라우팅 기능이 있지만, 바닐라 자바스크립트에서는 자체적인 라우팅이 없기에 브라우저에서 제공하는 `History api`를 사용해 라우팅을 처리할 수 있다.

# History API
> 브라우저가 관리하는 세션 히스토리로 사용자가 브라우저를 사용해 방문한 페이지들의 목록을 제얼할 수 있도록 HTML5가 제공하는 웹 API

## HTML.js
```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>History API</title>
</head>
<body>
    <h1>History API 예제</h1>
    <button id="page1">1 페이지 보기</button>
    <button id="page2">2 페이지 보기</button>
    <button id="page3">3 페이지 보기</button>
    
    <button id="goBack">뒤로 가기</button>
    <button id="goForward">앞으로 가기</button>

    <div id="content">여기에 페이지 내용이 표시</div>
    <script src ="/test/index.js"></script>
</body>
</html>
```

## index.js
```js
const changePage = (page) => {
    let $content = document.getElementById('content');
    $content.textContent = `현재 보고 있는 페이지는 ${page}입니다.`
    history.pushState({ page: page }, `Title ${page}`, `/${page}`);
}

window.addEventListener('popstate', (event) => {
    if (event.state) {
        let $content = document.getElementById('content');
        $content.textContent = `현재 보고 있는 페이지는 ${event.state.page} 입니다.`;
    }
})

document.getElementById('page1').addEventListener('click', () => {
    changePage('page1');
})
document.getElementById('page2').addEventListener('click', () => {
    changePage('page2');
})
document.getElementById('page3').addEventListener('click', () => {
    changePage('page3');
})

const goBack = () => {
    history.back();
}
const goForward = () => {
    history.forward();
}

document.getElementById('goBack').addEventListener('click', goBack);
document.getElementById('goForward').addEventListener('click', goForward);
```

### `changePage`
파라미터로 이동할 page를 받고, id가 content인 요소를 `$content`에 담아 텍스트를 입력

이후 `history`의 `pushState` 메서드를 이용하여 세션 히스토리에 현재 상태를 추가한다.

![](https://i.imgur.com/qFjgmdC.png)

![](https://i.imgur.com/CdlDxDt.png)

`history.pushState(state, title, url);`
state : 브라우저 이동 시 넘겨줄 데이터(popstate 에서 받아서 원하는 처리가능)
title : 변경할 브라우저 주소(변경을 원치 않으면 null)
url : 변경할 주소

state에 객체로 page, 제목은 `Title ${page}` , `url`은 `/${page}`를 전달

### `goBack` `goForward`

`history api`에 있는 `back()`과 `forward()`내장 함수를 이용하여 `click`이벤트 발생 시에 해당 기능 구현

### `window.addEventListener`

위에 `goBack`과 `goForward`만 하면 현재 보이는 page의 내용이 업데이트 되지 않는다.
이를 위해 `history api`가 제공하는 `popstate`이벤트를 사용
이는 히스토리의 값이 변경될 때, 발생되는 이벤트이다.

파라미터로 `event`를 받아서 `state`의 page 값을 이용하여 현재 페이지의 `content` id를 찾아서 텍스트를 변경

- 뒤로가기 버튼을 눌러서 console.log로 본 evnet
![](https://i.imgur.com/dCu0xvH.png)
