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

- HTML.js
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

- index.js
```js
```