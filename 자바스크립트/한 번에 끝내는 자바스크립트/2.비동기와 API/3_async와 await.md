> `async`와 `await`은 Promise 기반의 비동기 코드를 동기 코드 처럼 깔끔하게 작성할 수 있게 도와주는 문법

## `async` 
> `async`를 붙이면 **항상 Promise를 반환 하는 함수**
> 내부에서 return하면 자동으로 resolve() 된 Promise를 반환

```js
async function foo() {
  return 1;
}

foo().then((v) => {
  console.log(v);
})

1
```

## `await`
> `await` 는 Promise가 끝날 때 까지 기다렸다가 결과를 반환하며
> 반드시 `async` 함수 안에서만 사용 가능

```js
async function foo() {
  const result = await Promise.resolve(10);
  console.log(result);
  return result;
}

foo().then((v) => {
  console.log(v);
})

10
10
```

## then vs async/awit
### then
```js
fetch('https://api.example.com/data')
  .then((res) => res.json())
  .then((data) => {
    console.log(data);
  })
  .catch((err) => {
    console.error('에러 발생:', err);
  });
```
### async/awit
```
```