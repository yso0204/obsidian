지금까지 js에서 `this`는 함수 호출 방식에 따라 자동으로 결정된다는 알았지만, 다른 언어들에서 처럼 `this`를 그냥 해당 class나 객체에서 지정해서 사용하길 원할 때가 있다.

아래와 같은 방법으로 `this`를 강제로 할당할 수 있다.

# 예시
```js
const cafe = {
    brand: '스타벅스',
};

function printMenu(menu, size) {
    console.log(this);
    console.log(`${this.brand}의 ${menu} (${size})`);
}

printMenu(cafe, '아메리카노', '톨');
```
![](https://i.imgur.com/0GqlIp8.png)


현재 `this`는 `window`를 가리키고 있어 해당 값들이 정의되지 않앗다.

---

# `call()`

> 지금 이 객체(this)로 함수 실행해 라고 지정

`함수.call(지정할 this, 인자1, 인자2, ...)`

```js
const cafe = {
    brand: '스타벅스',
};

function printMenu(menu, size) {
    console.log(this);
    console.log(`${this.brand}의 ${menu} (${size})`);
}

printMenu.call(cafe, '아메리카노', '톨');
```
![](https://i.imgur.com/9C4yvGX.png)

비슷한 것으로 `apply()`가 있다.
# `apply()`
> `call()` 과 비슷하지만, 인자를 배열로 준다.

`함수.apply(지정할 this, [인자1, 인자2, ...])`
`printMenu.apply(cafe, ['카페라떼', '그란데']);` 로 실행
![](https://i.imgur.com/LwQ0wh8.png)


- `call()` 과 `apply()` 는 즉시 실행하는 특성이 있다.
- ---

# bind
> 이 객체(this) 와 묶은 함수를 새로 만들지만, call이나 apply 처럼 즉시 실행하는 것이 아님

`const 새함수 = 원본함수.bind(지정할 this, 인자....)`

- this와 인자를 미리 고정한 새 함수를 리턴만 하고 실행은 따로 해야한다.

```js
const sbMenu = printMenu.bind(cafe, '콜드브루', '벤티');
sbMenu();
```

또 다른 예시로 이전에 진행했던 타이머를 보자
## 타이머 예시
```js
function Counter() {
    this.count = 0;
    setInterval(function () {
        this.count++;
        console.log(this.count);
    }.bind(this),2000)
}
const counter = new Counter();
```
이렇게 bind로 `this`를 지정하여 count가 올라가는 것을 볼 수 있다.

`new Counter()`가 호출되어 아래 처럼 동작하는데
### `new` js 내부 동작

```js
let this = {};              // 새 객체 생성
this.__proto__ = Counter.prototype;
Counter.call(this);         // 이 this로 함수 실행
return this;
```
여기서 `ths.count = 0`은 `counter` 객체에 프로퍼티가 추가된다.

좀 더 자세히 살펴보면
1. 빈 객체 생성
`let this = {}` 로 this 라는 객체를 하나 만든다.
이 객체가 나중에 `counter` 객체가 된다.

2. 이 객체의 프로토 타입 연결
`this.__proto__ = Counter.prototype`
새 객체에 함수의 prototype을 연결해준다.
이로써 `counter`는 `Counter.prototype` 의 메서드에 접근할 수 있게 된다.

3. 생성자 함수 실행
`Counter.call(this)`
`Counter()` 함수 안의 `this`는 방금 만든 객체로 바인딩 된다.
그래서 `this.count = 0`같은 코드는 `this={count:0}` 이렇게 작동한다.

4. this 리턴
`return this`
생성자 함수가 명시적으로 객체를 반환하지 않으면, `new`는 자동으로 이 `this` 객체를 반환해준다.

```js
setInterval(function () {
    this.count++;
    console.log(this.count);
}.bind(this), 2000);
```
`setInterval`에서 this는 Counter의 내부 이므로 