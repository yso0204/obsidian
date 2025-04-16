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


## `json()`
그렇다면 data를 받아보려면 어떻게 해야할까?
```js
const getData = async () => {
  let response = await fetch('https://jsonplaceholder.typicode.com/users');
  let data = await response.json();
  console.log(response);
  console.log(data);
}

getData();
```

`async` 와 `await`로 보기 좋게 수정하고 
`fetch`로 받은 `Response`에는 json 형식의 data가 담겨있는데 `.json()`로 data를 파싱해서 받아보면
![](https://i.imgur.com/NSXOjH6.png)

이렇게 js가 사용할 수 있는 객체로 받아볼 수 있다.
이때 `fetch`는 비동기적으로 처리되기에 API가 호출이 완전히 끝난 후 await로 `.json()`을 이용해야한다.


## API 에러 핸들링
> API 호출은 네트워크를 통해 받기에 오류, 속도 등의 다양한 이유로 실패할 수 있다.
> 그렇기에 반드시 에러 처리가 필요하다

### `try...catch`
```js
const getData = async () => {
  try {
    let response = await fetch('https://jsonplaceholder.typicode.com/users');
    let data = await response.json();
    console.log(response);
    console.log(data);
  }
  catch {
    console.log(error);
  }
}

getData();
```