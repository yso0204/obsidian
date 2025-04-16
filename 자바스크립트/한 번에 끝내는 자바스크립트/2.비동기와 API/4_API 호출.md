# API

## 클라언트와 서버 통신
> 브라우저는 API를 통해서 서버에서 원하는 데이터를 요청하고 전달받는다


![](https://i.imgur.com/LyJseAb.png)

## `fetch`를 이용하여 API 호출 해보기
```js
let response = fetch('https://jsonplaceholder.typicode.com/users')
    .then((res) => console.log(res))
    .catch((err) => console.log(err));

console.log(response);
```

![](https://i.imgur.com/3nKG2Qy.png)

response가 먼저 출력되고(pending) 이후 resolve 된 값이 출력됨을 볼 수 있다.

그런데, 사이트에서 본 JSON 형태가 아닌 `response`가 출력 되었는데, `Response` 객체는 API 호출에 성공했을 때 반횐되는 API 성공 객체로 `fetch` 로 호출하면 API 성공 객체자체가 반환된다.


##