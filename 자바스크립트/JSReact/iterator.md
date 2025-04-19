# iterator
> 순차적으로 데이터를 하나씩 꺼낼 수 있는객체
> 배열, 문자열, Map, set 등이 iterable 이고
> for...of 같은 문법으로 순회 할 수 있는건 iterator를 구현하고 있기 때문이다.

## 기본개념
아래 두 가지 조건을 충족하는 객체
1. `next()` 메서드를 가지고 있다.
2. `next()`
를 호출하면 `{value: 값, doen: boolean}` 형태의 객체를 반환

`iterable` 객체는 반드시 `Symbol.iterator`라는 특별한 키를 가져야 한다.

## `Symbol.iterator`가 무엇인가?
> js 에서 반복할 수 있는 객체를`iterable`이라고 하는데 이 객체가 가지는 특별한 키

이 키에 대응하는 값은?
반복을 시작할 때 호출되는 함수

```js
const arr = [10, 20, 30];

console.log(typeof arr[Symbol.iterator]);

function
```

`const iterator = arr[Symbol.iterator]();`

이게 무슨 말이냐면, arr를 호출해서 반복을 시작하려면 arr의 `Symbol.iterator`함수 호출하면 iterator 객체가 나오고, 이 객체는 `.next()` 를 가지고 있다.

## Symbol 을 쓰는 이유?
일반적인 `iterator`를 쓰게되면 충돌 위험이 있다.
`Symbol.iterator` 는 전역적으로 유일한 심볼이라 다른 사람이 만든 코드랑 충돌할 일이 없고, js 엔진이 특별히 약속한 프로토콜로 인식할 수 있다.

예시
```js
const arr = [10, 20, 30];

const iterator= (arr[Symbol.iterator]());

console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());
console.log(iterator.next());

{ value: 10, done: false }
{ value: 20, done: false }
{ value: 30, done: false }
{ value: undefined, done: true }
```
- `arr[Symbol.iterator]()` iterator 객체 반환
- 이 객체는 `next()` 함수를 가짐
- `next()`를 호출할 때 마다 배열의 다음 값을 반환

```yaml
          [배열 arr]
              |
              | .[Symbol.iterator]()
              ↓
      [Iterator 객체 반환]  --> { next: function() { ... } }

              ↓
        next() 호출할 때마다
      { value: 요소값, done: false } 반환
              ↓
        끝나면 { done: true }
```

# 자바스크립트에서 for...of 동작
```js
const arr = [1, 2, 3];
for (const num of arr) {
    console.log(num);
}
```

위에 동작을 내부적으로 바라보면
```js
const arr = [1, 2, 3];

const iterator = arr[Symbol.iterator]();

while (true) {
    const result = iterator.next();
    if (result.done) break;
    const value = result.value;
    console.log(value);
    console.log(result);
}

1
{ value: 1, done: false }
2
{ value: 2, done: false }
3
{ value: 3, done: false }
```

결국 `for...of`는 위에 호출한 것과 마찬가지로 `iterator.next()`를 계속 호출해서 `next()`를 불러서 동작하고 있다.
